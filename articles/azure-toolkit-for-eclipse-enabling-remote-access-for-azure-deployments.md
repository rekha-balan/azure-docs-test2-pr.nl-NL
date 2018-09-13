---
title: Enabling Remote Access for Azure Deployments in Eclipse
description: Learn how to enable remote access for Azure deployments using the Azure Toolkit for Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: a2c88a7c7ad136184b8298dbcaeecb7e2314feb8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563564"
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="8a62c-103">Enabling Remote Access for Azure Deployments in Eclipse</span><span class="sxs-lookup"><span data-stu-id="8a62c-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="8a62c-104">To help troubleshoot your deployments, you may enable and use Remote Access to connect to the virtual machine hosting your deployment.</span><span class="sxs-lookup"><span data-stu-id="8a62c-104">To help troubleshoot your deployments, you may enable and use Remote Access to connect to the virtual machine hosting your deployment.</span></span> <span data-ttu-id="8a62c-105">The Remote Access functionality relies on the Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="8a62c-105">The Remote Access functionality relies on the Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="8a62c-106">You can configure Remote Access for your deployment after you have published it to Azure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish to Azure.</span><span class="sxs-lookup"><span data-stu-id="8a62c-106">You can configure Remote Access for your deployment after you have published it to Azure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish to Azure.</span></span> <span data-ttu-id="8a62c-107">Note that you will need a remote desktop client that is compatible with your operating system in order to connect to your deployment's virtual machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="8a62c-107">Note that you will need a remote desktop client that is compatible with your operating system in order to connect to your deployment's virtual machine in Azure.</span></span>

## <a name="how-to-enable-remote-access-before-you-deploy-to-azure"></a><span data-ttu-id="8a62c-108">How to enable Remote Access before you deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="8a62c-108">How to enable Remote Access before you deploy to Azure</span></span>
> [!NOTE]
> <span data-ttu-id="8a62c-109">To enable Remote Access before you deploy your application to Azure, you need to be running Eclipse on Windows.</span><span class="sxs-lookup"><span data-stu-id="8a62c-109">To enable Remote Access before you deploy your application to Azure, you need to be running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="8a62c-110">The following image shows the **Remote Access** properties dialog used to enable remote access.</span><span class="sxs-lookup"><span data-stu-id="8a62c-110">The following image shows the **Remote Access** properties dialog used to enable remote access.</span></span>

![][ic719494]

<span data-ttu-id="8a62c-111">There are two ways to display the **Remote Access** properties dialog:</span><span class="sxs-lookup"><span data-stu-id="8a62c-111">There are two ways to display the **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="8a62c-112">Click the **Advanced** link in the **Remote Access** section of the **Publish to Azure** dialog.</span><span class="sxs-lookup"><span data-stu-id="8a62c-112">Click the **Advanced** link in the **Remote Access** section of the **Publish to Azure** dialog.</span></span>
* <span data-ttu-id="8a62c-113">Open the **Properties** dialog of your Azure project.</span><span class="sxs-lookup"><span data-stu-id="8a62c-113">Open the **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="8a62c-114">When you create a new Azure deployment project, the project will not have Remote Access enabled by default.</span><span class="sxs-lookup"><span data-stu-id="8a62c-114">When you create a new Azure deployment project, the project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="8a62c-115">However, you can easily enable remote access by specifying the user name and password in the **Publish to Azure** dialog.</span><span class="sxs-lookup"><span data-stu-id="8a62c-115">However, you can easily enable remote access by specifying the user name and password in the **Publish to Azure** dialog.</span></span> <span data-ttu-id="8a62c-116">The Remote Access password is encrypted using X.509 certificates.</span><span class="sxs-lookup"><span data-stu-id="8a62c-116">The Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="8a62c-117">If you do not use provide your own certificate, the encryption relies on a self-signed certificate shipped with the Azure Plugin for Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8a62c-117">If you do not use provide your own certificate, the encryption relies on a self-signed certificate shipped with the Azure Plugin for Eclipse.</span></span> <span data-ttu-id="8a62c-118">This self-signed certificate is in the **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span><span class="sxs-lookup"><span data-stu-id="8a62c-118">This self-signed certificate is in the **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="8a62c-119">The latter contains the private key for the certificate, and it has a default password, **Password1**.</span><span class="sxs-lookup"><span data-stu-id="8a62c-119">The latter contains the private key for the certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="8a62c-120">However, since this password is public knowledge, the default certificate should be used only for learning purposes, not for a production deployment.</span><span class="sxs-lookup"><span data-stu-id="8a62c-120">However, since this password is public knowledge, the default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="8a62c-121">So other than for learning purposes, when you want to enabled remote sessions for your deployments, you should click the **Advanced** link in the **Publish to Azure** dialog to specify your own certificate.</span><span class="sxs-lookup"><span data-stu-id="8a62c-121">So other than for learning purposes, when you want to enabled remote sessions for your deployments, you should click the **Advanced** link in the **Publish to Azure** dialog to specify your own certificate.</span></span> <span data-ttu-id="8a62c-122">Note that you'll need to upload the PFX version of the certificate to your hosted service within the Azure Management Portal, so that Azure can decrypt the user password.</span><span class="sxs-lookup"><span data-stu-id="8a62c-122">Note that you'll need to upload the PFX version of the certificate to your hosted service within the Azure Management Portal, so that Azure can decrypt the user password.</span></span>

<span data-ttu-id="8a62c-123">The remainder of the tutorial shows you how to enable remote access for an Azure deployment project that was initially created with remote access disabled.</span><span class="sxs-lookup"><span data-stu-id="8a62c-123">The remainder of the tutorial shows you how to enable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="8a62c-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span><span class="sxs-lookup"><span data-stu-id="8a62c-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="8a62c-125">You also have the option of using a certificate issued by a certificate authority.</span><span class="sxs-lookup"><span data-stu-id="8a62c-125">You also have the option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-to-enable-remote-access-after-you-have-deployed-to-azure"></a><span data-ttu-id="8a62c-126">How to enable Remote Access after you have deployed to Azure</span><span class="sxs-lookup"><span data-stu-id="8a62c-126">How to enable Remote Access after you have deployed to Azure</span></span>
<span data-ttu-id="8a62c-127">To enable remote access after you have deployed to Azure, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="8a62c-127">To enable remote access after you have deployed to Azure, use the following steps:</span></span>

1. <span data-ttu-id="8a62c-128">Log into the Azure management portal using your Azure account</span><span class="sxs-lookup"><span data-stu-id="8a62c-128">Log into the Azure management portal using your Azure account</span></span>
2. <span data-ttu-id="8a62c-129">In your list of **Cloud Services**, select your deployed cloud service</span><span class="sxs-lookup"><span data-stu-id="8a62c-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>
3. <span data-ttu-id="8a62c-130">In the cloud service web page, click the **Configure** link</span><span class="sxs-lookup"><span data-stu-id="8a62c-130">In the cloud service web page, click the **Configure** link</span></span>
4. <span data-ttu-id="8a62c-131">On the bottom of the configuration page, click the **Remote** link</span><span class="sxs-lookup"><span data-stu-id="8a62c-131">On the bottom of the configuration page, click the **Remote** link</span></span>
5. <span data-ttu-id="8a62c-132">When the pop-up dialog box appears:</span><span class="sxs-lookup"><span data-stu-id="8a62c-132">When the pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="8a62c-133">Specify the Role you for which you want to enable remote access</span><span class="sxs-lookup"><span data-stu-id="8a62c-133">Specify the Role you for which you want to enable remote access</span></span>
   * <span data-ttu-id="8a62c-134">Click to select the **Enable Remote Desktop** checkbox</span><span class="sxs-lookup"><span data-stu-id="8a62c-134">Click to select the **Enable Remote Desktop** checkbox</span></span>
   * <span data-ttu-id="8a62c-135">Specify a user name and password you want to use for remote access</span><span class="sxs-lookup"><span data-stu-id="8a62c-135">Specify a user name and password you want to use for remote access</span></span>
   * <span data-ttu-id="8a62c-136">Select the certificate to use</span><span class="sxs-lookup"><span data-stu-id="8a62c-136">Select the certificate to use</span></span>
6. <span data-ttu-id="8a62c-137">Click **OK**</span><span class="sxs-lookup"><span data-stu-id="8a62c-137">Click **OK**</span></span> 

<span data-ttu-id="8a62c-138">You will see a message stating that your configuration change is in progress, which may take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="8a62c-138">You will see a message stating that your configuration change is in progress, which may take a few minutes to complete.</span></span> <span data-ttu-id="8a62c-139">After the configuration change has completed, follow the steps in the **To log in remotely** section later in this article.</span><span class="sxs-lookup"><span data-stu-id="8a62c-139">After the configuration change has completed, follow the steps in the **To log in remotely** section later in this article.</span></span>

## <a name="how-to-enable-remote-access-in-your-package"></a><span data-ttu-id="8a62c-140">How to enable Remote Access in your package</span><span class="sxs-lookup"><span data-stu-id="8a62c-140">How to enable Remote Access in your package</span></span>
1. <span data-ttu-id="8a62c-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="8a62c-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>
2. <span data-ttu-id="8a62c-142">In the **Properties** dialog, expand **Azure** in the left-hand pane and click **Remote Access**.</span><span class="sxs-lookup"><span data-stu-id="8a62c-142">In the **Properties** dialog, expand **Azure** in the left-hand pane and click **Remote Access**.</span></span>
3. <span data-ttu-id="8a62c-143">In the **Remote Access** dialog, ensure **Enable all roles to accept Remote Desktop Connections with these login credentials** is checked.</span><span class="sxs-lookup"><span data-stu-id="8a62c-143">In the **Remote Access** dialog, ensure **Enable all roles to accept Remote Desktop Connections with these login credentials** is checked.</span></span>
4. <span data-ttu-id="8a62c-144">Specify a user name for the Remote Desktop connection.</span><span class="sxs-lookup"><span data-stu-id="8a62c-144">Specify a user name for the Remote Desktop connection.</span></span>
5. <span data-ttu-id="8a62c-145">Specify and confirm the password for the user.</span><span class="sxs-lookup"><span data-stu-id="8a62c-145">Specify and confirm the password for the user.</span></span> <span data-ttu-id="8a62c-146">The user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span><span class="sxs-lookup"><span data-stu-id="8a62c-146">The user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="8a62c-147">(Note that this is a separate password from your PFX password.)</span><span class="sxs-lookup"><span data-stu-id="8a62c-147">(Note that this is a separate password from your PFX password.)</span></span>
6. <span data-ttu-id="8a62c-148">Specify the expiration date for the user account.</span><span class="sxs-lookup"><span data-stu-id="8a62c-148">Specify the expiration date for the user account.</span></span>
7. <span data-ttu-id="8a62c-149">Click **New** to create a new self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="8a62c-149">Click **New** to create a new self-signed certificate.</span></span> <span data-ttu-id="8a62c-150">(Alternatively, you could select a certificate from your workspace or file system through the **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span><span class="sxs-lookup"><span data-stu-id="8a62c-150">(Alternatively, you could select a certificate from your workspace or file system through the **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>
   
   * <span data-ttu-id="8a62c-151">In the **New Certificate** dialog, specify and confirm the password you'll use for your PFX file.</span><span class="sxs-lookup"><span data-stu-id="8a62c-151">In the **New Certificate** dialog, specify and confirm the password you'll use for your PFX file.</span></span>
   * <span data-ttu-id="8a62c-152">Accept the value provided for **Name (CN)**, or use a custom name.</span><span class="sxs-lookup"><span data-stu-id="8a62c-152">Accept the value provided for **Name (CN)**, or use a custom name.</span></span>
   * <span data-ttu-id="8a62c-153">Specify the path and file name where the new certificate, in .cer form, will be saved.</span><span class="sxs-lookup"><span data-stu-id="8a62c-153">Specify the path and file name where the new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="8a62c-154">For this step and the next step, you could use the **cert** folder of your Azure project, but you're free to choose another location.</span><span class="sxs-lookup"><span data-stu-id="8a62c-154">For this step and the next step, you could use the **cert** folder of your Azure project, but you're free to choose another location.</span></span> <span data-ttu-id="8a62c-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span><span class="sxs-lookup"><span data-stu-id="8a62c-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="8a62c-156">(Create the **c:\mycert** folder prior to proceeding, or use an existing folder if desired.)</span><span class="sxs-lookup"><span data-stu-id="8a62c-156">(Create the **c:\mycert** folder prior to proceeding, or use an existing folder if desired.)</span></span>
   * <span data-ttu-id="8a62c-157">Specify the path and file name where the new certificate and its private key, in .pfx form, will be saved.</span><span class="sxs-lookup"><span data-stu-id="8a62c-157">Specify the path and file name where the new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="8a62c-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="8a62c-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="8a62c-159">Your **New Certificate** dialog should look similar to the following (update the folder paths if you did not use **c:\mycert**):</span><span class="sxs-lookup"><span data-stu-id="8a62c-159">Your **New Certificate** dialog should look similar to the following (update the folder paths if you did not use **c:\mycert**):</span></span>
     
       ![][ic712275]
   * <span data-ttu-id="8a62c-160">Click **OK** to close the **New Certificate** dialog.</span><span class="sxs-lookup"><span data-stu-id="8a62c-160">Click **OK** to close the **New Certificate** dialog.</span></span>
8. <span data-ttu-id="8a62c-161">Your **Remote Access** dialog should look similar to the following:</span><span class="sxs-lookup"><span data-stu-id="8a62c-161">Your **Remote Access** dialog should look similar to the following:</span></span></p>
   
    ![][ic719495]
9. <span data-ttu-id="8a62c-162">Click **OK** to close the **Remote Access** dialog.</span><span class="sxs-lookup"><span data-stu-id="8a62c-162">Click **OK** to close the **Remote Access** dialog.</span></span>

<span data-ttu-id="8a62c-163">Rebuild your application, with the build set for deployment to cloud.</span><span class="sxs-lookup"><span data-stu-id="8a62c-163">Rebuild your application, with the build set for deployment to cloud.</span></span>

## <a name="to-log-in-remotely"></a><span data-ttu-id="8a62c-164">To log in remotely</span><span class="sxs-lookup"><span data-stu-id="8a62c-164">To log in remotely</span></span>
<span data-ttu-id="8a62c-165">Once your role instance is ready, you can remotely log in to the virtual machine that is hosting your application.</span><span class="sxs-lookup"><span data-stu-id="8a62c-165">Once your role instance is ready, you can remotely log in to the virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="8a62c-166">If are using Eclipse on Windows and you selected the **Start remote desktop on deploy** option during your deployment to Azure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span><span class="sxs-lookup"><span data-stu-id="8a62c-166">If are using Eclipse on Windows and you selected the **Start remote desktop on deploy** option during your deployment to Azure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="8a62c-167">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span><span class="sxs-lookup"><span data-stu-id="8a62c-167">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>
* <span data-ttu-id="8a62c-168">Another way to log in remotely is through the <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span><span class="sxs-lookup"><span data-stu-id="8a62c-168">Another way to log in remotely is through the <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="8a62c-169">Within the **Cloud Services** view of the Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click the **Connect** button.</span><span class="sxs-lookup"><span data-stu-id="8a62c-169">Within the **Cloud Services** view of the Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click the **Connect** button.</span></span> <span data-ttu-id="8a62c-170">The **Connect** button appears as the following in the command bar:</span><span class="sxs-lookup"><span data-stu-id="8a62c-170">The **Connect** button appears as the following in the command bar:</span></span>
    
      ![][ic659273]
  * <span data-ttu-id="8a62c-171">After clicking the **Connect** button, you will be prompted to open an RDP file.</span><span class="sxs-lookup"><span data-stu-id="8a62c-171">After clicking the **Connect** button, you will be prompted to open an RDP file.</span></span> <span data-ttu-id="8a62c-172">Open the file and follow the prompts.</span><span class="sxs-lookup"><span data-stu-id="8a62c-172">Open the file and follow the prompts.</span></span> <span data-ttu-id="8a62c-173">(You could also save this file to your local computer, and then run the file by double-clicking it to remote log in to your virtual machine without needing to first go the management portal.)</span><span class="sxs-lookup"><span data-stu-id="8a62c-173">(You could also save this file to your local computer, and then run the file by double-clicking it to remote log in to your virtual machine without needing to first go the management portal.)</span></span>
  * <span data-ttu-id="8a62c-174">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span><span class="sxs-lookup"><span data-stu-id="8a62c-174">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

> [!NOTE]
> <span data-ttu-id="8a62c-175">If you are on a non-Windows operating system, you need to use a Remote Desktop client that is compatible with your operating system and follow the steps to configure that client with the settings in the RDP file that you downloaded.</span><span class="sxs-lookup"><span data-stu-id="8a62c-175">If you are on a non-Windows operating system, you need to use a Remote Desktop client that is compatible with your operating system and follow the steps to configure that client with the settings in the RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="8a62c-176">See Also</span><span class="sxs-lookup"><span data-stu-id="8a62c-176">See Also</span></span>
<span data-ttu-id="8a62c-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8a62c-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="8a62c-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8a62c-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="8a62c-179">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8a62c-179">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="8a62c-180">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="8a62c-180">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->




