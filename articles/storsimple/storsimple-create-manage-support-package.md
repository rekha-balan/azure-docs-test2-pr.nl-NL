---
title: Create a StorSimple support package | Microsoft Docs
description: Learn how to create, decrypt, and edit a support package for your StorSimple device.
services: storsimple
documentationcenter: ''
author: alkohli
manager: carmonm
editor: ''
ms.assetid: eac76f5f-5db1-4c92-af8c-54053b91e66c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e51cd182e190d2074025c9c05b4e778b6da6a87c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562959"
---
# <a name="create-and-manage-a-storsimple-support-package"></a><span data-ttu-id="11436-103">Create and manage a StorSimple support package</span><span class="sxs-lookup"><span data-stu-id="11436-103">Create and manage a StorSimple support package</span></span>
## <a name="overview"></a><span data-ttu-id="11436-104">Overview</span><span class="sxs-lookup"><span data-stu-id="11436-104">Overview</span></span>
<span data-ttu-id="11436-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs to assist Microsoft Support with troubleshooting any StorSimple device issues.</span><span class="sxs-lookup"><span data-stu-id="11436-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs to assist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="11436-106">The collected logs are encrypted and compressed.</span><span class="sxs-lookup"><span data-stu-id="11436-106">The collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="11436-107">This tutorial includes step-by-step instructions to create and manage the support package.</span><span class="sxs-lookup"><span data-stu-id="11436-107">This tutorial includes step-by-step instructions to create and manage the support package.</span></span>

## <a name="create-and-upload-a-support-package-in-the-azure-classic-portal"></a><span data-ttu-id="11436-108">Create and upload a support package in the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="11436-108">Create and upload a support package in the Azure classic portal</span></span>
<span data-ttu-id="11436-109">You can create and upload a support package to the Microsoft Support site through the **Maintenance** page of the service in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="11436-109">You can create and upload a support package to the Microsoft Support site through the **Maintenance** page of the service in the Azure classic portal.</span></span>

> [!NOTE]
> <span data-ttu-id="11436-110">The upload requires a support passkey.</span><span class="sxs-lookup"><span data-stu-id="11436-110">The upload requires a support passkey.</span></span> <span data-ttu-id="11436-111">Your support engineer should provide this to you in an email.</span><span class="sxs-lookup"><span data-stu-id="11436-111">Your support engineer should provide this to you in an email.</span></span>
> 
> 

<span data-ttu-id="11436-112">An encrypted and compressed support package (.cab file) is created and uploaded to the Support site.</span><span class="sxs-lookup"><span data-stu-id="11436-112">An encrypted and compressed support package (.cab file) is created and uploaded to the Support site.</span></span> <span data-ttu-id="11436-113">The support engineer can then retrieve this package from the Support site for troubleshooting the issue.</span><span class="sxs-lookup"><span data-stu-id="11436-113">The support engineer can then retrieve this package from the Support site for troubleshooting the issue.</span></span>

<span data-ttu-id="11436-114">Perform the following steps in the classic portal to create a support package.</span><span class="sxs-lookup"><span data-stu-id="11436-114">Perform the following steps in the classic portal to create a support package.</span></span>

#### <a name="to-create-a-support-package-in-the-azure-classic-portal"></a><span data-ttu-id="11436-115">To create a support package in the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="11436-115">To create a support package in the Azure classic portal</span></span>
1. <span data-ttu-id="11436-116">Select **Devices** > **Maintenance**.</span><span class="sxs-lookup"><span data-stu-id="11436-116">Select **Devices** > **Maintenance**.</span></span>
2. <span data-ttu-id="11436-117">In the **Support package** section, select **Create and upload support package**.</span><span class="sxs-lookup"><span data-stu-id="11436-117">In the **Support package** section, select **Create and upload support package**.</span></span>
3. <span data-ttu-id="11436-118">In the **Create and upload support package** dialog box, do the following:</span><span class="sxs-lookup"><span data-stu-id="11436-118">In the **Create and upload support package** dialog box, do the following:</span></span>
   
    ![Create support package](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-create-manage-support-package/IC740923.png)
   
   * <span data-ttu-id="11436-120">In the **Support Passkey** text box, enter the passkey.</span><span class="sxs-lookup"><span data-stu-id="11436-120">In the **Support Passkey** text box, enter the passkey.</span></span> <span data-ttu-id="11436-121">Your Microsoft support engineer should send this passkey to you in email.</span><span class="sxs-lookup"><span data-stu-id="11436-121">Your Microsoft support engineer should send this passkey to you in email.</span></span>
   * <span data-ttu-id="11436-122">Select the check box to provide consent to automatically upload the support package to the Microsoft Support site.</span><span class="sxs-lookup"><span data-stu-id="11436-122">Select the check box to provide consent to automatically upload the support package to the Microsoft Support site.</span></span>
   * <span data-ttu-id="11436-123">Click the check icon</span><span class="sxs-lookup"><span data-stu-id="11436-123">Click the check icon</span></span> ![Check icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-create-manage-support-package/IC740895.png)<span data-ttu-id="11436-125">.</span><span class="sxs-lookup"><span data-stu-id="11436-125">.</span></span>

## <a name="manually-create-a-support-package"></a><span data-ttu-id="11436-126">Manually create a support package</span><span class="sxs-lookup"><span data-stu-id="11436-126">Manually create a support package</span></span>
<span data-ttu-id="11436-127">In some cases, you'll need to manually create the support package through Windows PowerShell for StorSimple.</span><span class="sxs-lookup"><span data-stu-id="11436-127">In some cases, you'll need to manually create the support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="11436-128">For example:</span><span class="sxs-lookup"><span data-stu-id="11436-128">For example:</span></span>

* <span data-ttu-id="11436-129">If you need to remove sensitive information from your log files prior to sharing with Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="11436-129">If you need to remove sensitive information from your log files prior to sharing with Microsoft Support.</span></span>
* <span data-ttu-id="11436-130">If you are having difficulty uploading the package due to connectivity issues.</span><span class="sxs-lookup"><span data-stu-id="11436-130">If you are having difficulty uploading the package due to connectivity issues.</span></span>

<span data-ttu-id="11436-131">You can share your manually generated support package with Microsoft Support over email.</span><span class="sxs-lookup"><span data-stu-id="11436-131">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="11436-132">Perform the following steps to create a support package in Windows PowerShell for StorSimple.</span><span class="sxs-lookup"><span data-stu-id="11436-132">Perform the following steps to create a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="to-create-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="11436-133">To create a support package in Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="11436-133">To create a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="11436-134">To start a Windows PowerShell session as an administrator on the remote computer that's used to connect to your StorSimple device, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="11436-134">To start a Windows PowerShell session as an administrator on the remote computer that's used to connect to your StorSimple device, enter the following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="11436-135">In the Windows PowerShell session, connect to the SSAdmin Console of your device:</span><span class="sxs-lookup"><span data-stu-id="11436-135">In the Windows PowerShell session, connect to the SSAdmin Console of your device:</span></span>
   
   * <span data-ttu-id="11436-136">At the command prompt, enter:</span><span class="sxs-lookup"><span data-stu-id="11436-136">At the command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * <span data-ttu-id="11436-137">In the dialog box that opens, enter your device administrator password.</span><span class="sxs-lookup"><span data-stu-id="11436-137">In the dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="11436-138">The default password is:</span><span class="sxs-lookup"><span data-stu-id="11436-138">The default password is:</span></span>
     
      `Password1`
     
      ![PowerShell credential dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-create-manage-support-package/IC740962.png)
   * <span data-ttu-id="11436-140">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="11436-140">Select **OK**.</span></span>
   * <span data-ttu-id="11436-141">At the command prompt, enter:</span><span class="sxs-lookup"><span data-stu-id="11436-141">At the command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="11436-142">In the session that opens, enter the appropriate command.</span><span class="sxs-lookup"><span data-stu-id="11436-142">In the session that opens, enter the appropriate command.</span></span>
   
   * <span data-ttu-id="11436-143">For network shares that are password protected, enter:</span><span class="sxs-lookup"><span data-stu-id="11436-143">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="11436-144">You'll be prompted for a password, a path to the network shared folder, and an encryption passphrase (because the support package is encrypted).</span><span class="sxs-lookup"><span data-stu-id="11436-144">You'll be prompted for a password, a path to the network shared folder, and an encryption passphrase (because the support package is encrypted).</span></span> <span data-ttu-id="11436-145">A support package is then created in the specified folder.</span><span class="sxs-lookup"><span data-stu-id="11436-145">A support package is then created in the specified folder.</span></span>
   * <span data-ttu-id="11436-146">For shares that are not password protected, you do not need the `-Credential` parameter.</span><span class="sxs-lookup"><span data-stu-id="11436-146">For shares that are not password protected, you do not need the `-Credential` parameter.</span></span> <span data-ttu-id="11436-147">Enter the following:</span><span class="sxs-lookup"><span data-stu-id="11436-147">Enter the following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="11436-148">The support package is created for both controllers in the specified network shared folder.</span><span class="sxs-lookup"><span data-stu-id="11436-148">The support package is created for both controllers in the specified network shared folder.</span></span> <span data-ttu-id="11436-149">It's an encrypted, compressed file that can be sent to Microsoft Support for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="11436-149">It's an encrypted, compressed file that can be sent to Microsoft Support for troubleshooting.</span></span> <span data-ttu-id="11436-150">For more information, see [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="11436-150">For more information, see [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

### <a name="the-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="11436-151">The Export-HcsSupportPackage cmdlet parameters</span><span class="sxs-lookup"><span data-stu-id="11436-151">The Export-HcsSupportPackage cmdlet parameters</span></span>
<span data-ttu-id="11436-152">You can use the following parameters with the Export-HcsSupportPackage cmdlet.</span><span class="sxs-lookup"><span data-stu-id="11436-152">You can use the following parameters with the Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="11436-153">Parameter</span><span class="sxs-lookup"><span data-stu-id="11436-153">Parameter</span></span> | <span data-ttu-id="11436-154">Required/Optional</span><span class="sxs-lookup"><span data-stu-id="11436-154">Required/Optional</span></span> | <span data-ttu-id="11436-155">Description</span><span class="sxs-lookup"><span data-stu-id="11436-155">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="11436-156">Required</span><span class="sxs-lookup"><span data-stu-id="11436-156">Required</span></span> |<span data-ttu-id="11436-157">Use to provide the location of the network shared folder in which the support package is placed.</span><span class="sxs-lookup"><span data-stu-id="11436-157">Use to provide the location of the network shared folder in which the support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="11436-158">Required</span><span class="sxs-lookup"><span data-stu-id="11436-158">Required</span></span> |<span data-ttu-id="11436-159">Use to provide a passphrase to help encrypt the support package.</span><span class="sxs-lookup"><span data-stu-id="11436-159">Use to provide a passphrase to help encrypt the support package.</span></span> |
| `-Credential` |<span data-ttu-id="11436-160">Optional</span><span class="sxs-lookup"><span data-stu-id="11436-160">Optional</span></span> |<span data-ttu-id="11436-161">Use to supply access credentials for the network shared folder.</span><span class="sxs-lookup"><span data-stu-id="11436-161">Use to supply access credentials for the network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="11436-162">Optional</span><span class="sxs-lookup"><span data-stu-id="11436-162">Optional</span></span> |<span data-ttu-id="11436-163">Use to skip the encryption passphrase confirmation step.</span><span class="sxs-lookup"><span data-stu-id="11436-163">Use to skip the encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="11436-164">Optional</span><span class="sxs-lookup"><span data-stu-id="11436-164">Optional</span></span> |<span data-ttu-id="11436-165">Use to specify a directory under *Path* in which the support package is placed.</span><span class="sxs-lookup"><span data-stu-id="11436-165">Use to specify a directory under *Path* in which the support package is placed.</span></span> <span data-ttu-id="11436-166">The default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span><span class="sxs-lookup"><span data-stu-id="11436-166">The default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="11436-167">Optional</span><span class="sxs-lookup"><span data-stu-id="11436-167">Optional</span></span> |<span data-ttu-id="11436-168">Specify as **Cluster** (default) to create a support package for both controllers.</span><span class="sxs-lookup"><span data-stu-id="11436-168">Specify as **Cluster** (default) to create a support package for both controllers.</span></span> <span data-ttu-id="11436-169">If you want to create a package only for the current controller, specify **Controller**.</span><span class="sxs-lookup"><span data-stu-id="11436-169">If you want to create a package only for the current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="11436-170">Edit a support package</span><span class="sxs-lookup"><span data-stu-id="11436-170">Edit a support package</span></span>
<span data-ttu-id="11436-171">After you have generated a support package, you might need to edit the package to remove sensitive information.</span><span class="sxs-lookup"><span data-stu-id="11436-171">After you have generated a support package, you might need to edit the package to remove sensitive information.</span></span> <span data-ttu-id="11436-172">This can include volume names, device IP addresses, and backup names from the log files.</span><span class="sxs-lookup"><span data-stu-id="11436-172">This can include volume names, device IP addresses, and backup names from the log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11436-173">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span><span class="sxs-lookup"><span data-stu-id="11436-173">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="11436-174">You can't edit a package created in the Azure classic portal with StorSimple Manager service.</span><span class="sxs-lookup"><span data-stu-id="11436-174">You can't edit a package created in the Azure classic portal with StorSimple Manager service.</span></span>
> 
> 

<span data-ttu-id="11436-175">To edit a support package before uploading it on the Microsoft Support site, first decrypt the support package, edit the files, and then re-encrypt it.</span><span class="sxs-lookup"><span data-stu-id="11436-175">To edit a support package before uploading it on the Microsoft Support site, first decrypt the support package, edit the files, and then re-encrypt it.</span></span> <span data-ttu-id="11436-176">Perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="11436-176">Perform the following steps.</span></span>

#### <a name="to-edit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="11436-177">To edit a support package in Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="11436-177">To edit a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="11436-178">Generate a support package as described earlier, in [To create a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="11436-178">Generate a support package as described earlier, in [To create a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="11436-179">[Download the script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span><span class="sxs-lookup"><span data-stu-id="11436-179">[Download the script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="11436-180">Import the Windows PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="11436-180">Import the Windows PowerShell module.</span></span> <span data-ttu-id="11436-181">Specify the path to the local folder in which you downloaded the script.</span><span class="sxs-lookup"><span data-stu-id="11436-181">Specify the path to the local folder in which you downloaded the script.</span></span> <span data-ttu-id="11436-182">To import the module, enter:</span><span class="sxs-lookup"><span data-stu-id="11436-182">To import the module, enter:</span></span>
   
    `Import-module <Path to the folder that contains the Windows PowerShell script>`
4. <span data-ttu-id="11436-183">All the files are *.aes* files that are compressed and encrypted.</span><span class="sxs-lookup"><span data-stu-id="11436-183">All the files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="11436-184">To decompress and decrypt files, enter:</span><span class="sxs-lookup"><span data-stu-id="11436-184">To decompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path to the folder that contains support package files>`
   
    <span data-ttu-id="11436-185">Note that the actual file extensions are now displayed for all the files.</span><span class="sxs-lookup"><span data-stu-id="11436-185">Note that the actual file extensions are now displayed for all the files.</span></span>
   
    ![Edit support package](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="11436-187">When you're prompted for the encryption passphrase, enter the passphrase that you used when the support package was created.</span><span class="sxs-lookup"><span data-stu-id="11436-187">When you're prompted for the encryption passphrase, enter the passphrase that you used when the support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for the following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="11436-188">Browse to the folder that contains the log files.</span><span class="sxs-lookup"><span data-stu-id="11436-188">Browse to the folder that contains the log files.</span></span> <span data-ttu-id="11436-189">Because the log files are now decompressed and decrypted, these will have original file extensions.</span><span class="sxs-lookup"><span data-stu-id="11436-189">Because the log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="11436-190">Modify these files to remove any customer-specific information, such as volume names and device IP addresses, and save the files.</span><span class="sxs-lookup"><span data-stu-id="11436-190">Modify these files to remove any customer-specific information, such as volume names and device IP addresses, and save the files.</span></span>
7. <span data-ttu-id="11436-191">Close the files to compress them with gzip and encrypt them with AES-256.</span><span class="sxs-lookup"><span data-stu-id="11436-191">Close the files to compress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="11436-192">This is for speed and security in transferring the support package over a network.</span><span class="sxs-lookup"><span data-stu-id="11436-192">This is for speed and security in transferring the support package over a network.</span></span> <span data-ttu-id="11436-193">To compress and encrypt files, enter the following:</span><span class="sxs-lookup"><span data-stu-id="11436-193">To compress and encrypt files, enter the following:</span></span>
   
    `Close-HcsSupportPackage <Path to the folder that contains support package files>`
   
    ![Edit support package](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="11436-195">When prompted, provide an encryption passphrase for the modified support package.</span><span class="sxs-lookup"><span data-stu-id="11436-195">When prompted, provide an encryption passphrase for the modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for the following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="11436-196">Write down the new passphrase, so that you can share it with Microsoft Support when requested.</span><span class="sxs-lookup"><span data-stu-id="11436-196">Write down the new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="11436-197">Example: Editing files in a support package on a password-protected share</span><span class="sxs-lookup"><span data-stu-id="11436-197">Example: Editing files in a support package on a password-protected share</span></span>
<span data-ttu-id="11436-198">The following example shows how to decrypt, edit, and re-encrypt a support package.</span><span class="sxs-lookup"><span data-stu-id="11436-198">The following example shows how to decrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="11436-199">Next steps</span><span class="sxs-lookup"><span data-stu-id="11436-199">Next steps</span></span>
* <span data-ttu-id="11436-200">Learn how to [use support packages and device logs to troubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="11436-200">Learn how to [use support packages and device logs to troubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="11436-201">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="11436-201">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>






