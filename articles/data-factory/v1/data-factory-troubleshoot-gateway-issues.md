---
title: Troubleshoot Data Management Gateway issues | Microsoft Docs
description: Provides tips to troubleshoot issues related to Data Management Gateway.
services: data-factory
author: nabhishek
manager: craigg
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 10/01/2017
ms.author: abnarain
robots: noindex
ms.openlocfilehash: 9453099af8d9be21a97808733ffa8f8bfe5a364a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870779"
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a><span data-ttu-id="b4ad7-103">Troubleshoot issues with using Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="b4ad7-103">Troubleshoot issues with using Data Management Gateway</span></span>
<span data-ttu-id="b4ad7-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="b4ad7-105">This article applies to version 1 of Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-105">This article applies to version 1 of Azure Data Factory.</span></span> <span data-ttu-id="b4ad7-106">If you are using the current version of the Data Factory service, see [self-hosted integration runtime in Data Factory](../create-self-hosted-integration-runtime.md).</span><span class="sxs-lookup"><span data-stu-id="b4ad7-106">If you are using the current version of the Data Factory service, see [self-hosted integration runtime in Data Factory](../create-self-hosted-integration-runtime.md).</span></span>

<span data-ttu-id="b4ad7-107">See the [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about the gateway.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-107">See the [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about the gateway.</span></span> <span data-ttu-id="b4ad7-108">See the [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database to Microsoft Azure Blob storage by using the gateway.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-108">See the [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database to Microsoft Azure Blob storage by using the gateway.</span></span>

## <a name="failed-to-install-or-register-gateway"></a><span data-ttu-id="b4ad7-109">Failed to install or register gateway</span><span class="sxs-lookup"><span data-stu-id="b4ad7-109">Failed to install or register gateway</span></span>
### <a name="1-problem"></a><span data-ttu-id="b4ad7-110">1. Problem</span><span class="sxs-lookup"><span data-stu-id="b4ad7-110">1. Problem</span></span>
<span data-ttu-id="b4ad7-111">You see this error message when installing and registering a gateway, specifically, while downloading the gateway installation file.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-111">You see this error message when installing and registering a gateway, specifically, while downloading the gateway installation file.</span></span>

`Unable to connect to the remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a><span data-ttu-id="b4ad7-112">Cause</span><span class="sxs-lookup"><span data-stu-id="b4ad7-112">Cause</span></span>
<span data-ttu-id="b4ad7-113">The machine on which you are trying to install the gateway has failed to download the latest gateway installation file from the download center due to a network issue.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-113">The machine on which you are trying to install the gateway has failed to download the latest gateway installation file from the download center due to a network issue.</span></span>

#### <a name="resolution"></a><span data-ttu-id="b4ad7-114">Resolution</span><span class="sxs-lookup"><span data-stu-id="b4ad7-114">Resolution</span></span>
<span data-ttu-id="b4ad7-115">Check your firewall proxy server settings to see whether the settings block the network connection from the computer to the [download center](https://download.microsoft.com/), and update the settings accordingly.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-115">Check your firewall proxy server settings to see whether the settings block the network connection from the computer to the [download center](https://download.microsoft.com/), and update the settings accordingly.</span></span>

<span data-ttu-id="b4ad7-116">Alternatively, you can download the installation file for the latest gateway from the [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access the download center.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-116">Alternatively, you can download the installation file for the latest gateway from the [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access the download center.</span></span> <span data-ttu-id="b4ad7-117">You can then copy the installer file to the gateway host computer and run it manually to install and update the gateway.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-117">You can then copy the installer file to the gateway host computer and run it manually to install and update the gateway.</span></span>

### <a name="2-problem"></a><span data-ttu-id="b4ad7-118">2. Problem</span><span class="sxs-lookup"><span data-stu-id="b4ad7-118">2. Problem</span></span>
<span data-ttu-id="b4ad7-119">You see this error when you're attempting to install a gateway by clicking **install directly on this computer** in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-119">You see this error when you're attempting to install a gateway by clicking **install directly on this computer** in the Azure portal.</span></span>

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a><span data-ttu-id="b4ad7-120">Cause</span><span class="sxs-lookup"><span data-stu-id="b4ad7-120">Cause</span></span>
<span data-ttu-id="b4ad7-121">A gateway is already installed on the machine.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-121">A gateway is already installed on the machine.</span></span>

#### <a name="resolution"></a><span data-ttu-id="b4ad7-122">Resolution</span><span class="sxs-lookup"><span data-stu-id="b4ad7-122">Resolution</span></span>
<span data-ttu-id="b4ad7-123">Uninstall the existing gateway on the machine and click the **install directly on this computer** link again.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-123">Uninstall the existing gateway on the machine and click the **install directly on this computer** link again.</span></span>

### <a name="3-problem"></a><span data-ttu-id="b4ad7-124">3. Problem</span><span class="sxs-lookup"><span data-stu-id="b4ad7-124">3. Problem</span></span>
<span data-ttu-id="b4ad7-125">You might see this error when registering a new gateway.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-125">You might see this error when registering a new gateway.</span></span>

`Error: The gateway has encountered an error during registration.`

#### <a name="cause"></a><span data-ttu-id="b4ad7-126">Cause</span><span class="sxs-lookup"><span data-stu-id="b4ad7-126">Cause</span></span>
<span data-ttu-id="b4ad7-127">You might see this message for one of the following reasons:</span><span class="sxs-lookup"><span data-stu-id="b4ad7-127">You might see this message for one of the following reasons:</span></span>

* <span data-ttu-id="b4ad7-128">The format of the gateway key is invalid.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-128">The format of the gateway key is invalid.</span></span>
* <span data-ttu-id="b4ad7-129">The gateway key has been invalidated.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-129">The gateway key has been invalidated.</span></span>
* <span data-ttu-id="b4ad7-130">The gateway key has been regenerated from the portal.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-130">The gateway key has been regenerated from the portal.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="b4ad7-131">Resolution</span><span class="sxs-lookup"><span data-stu-id="b4ad7-131">Resolution</span></span>
<span data-ttu-id="b4ad7-132">Verify whether you are using the right gateway key from the portal.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-132">Verify whether you are using the right gateway key from the portal.</span></span> <span data-ttu-id="b4ad7-133">If needed, regenerate a key and use the key to register the gateway.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-133">If needed, regenerate a key and use the key to register the gateway.</span></span>

### <a name="4-problem"></a><span data-ttu-id="b4ad7-134">4. Problem</span><span class="sxs-lookup"><span data-stu-id="b4ad7-134">4. Problem</span></span>
<span data-ttu-id="b4ad7-135">You might see the following error message when you're registering a gateway.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-135">You might see the following error message when you're registering a gateway.</span></span>

`Error: The content or format of the gateway key "{gatewayKey}" is invalid, please go to azure portal to create one new gateway or regenerate the gateway key.`



![Content or format of key is invalid](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a><span data-ttu-id="b4ad7-137">Cause</span><span class="sxs-lookup"><span data-stu-id="b4ad7-137">Cause</span></span>
<span data-ttu-id="b4ad7-138">The content or format of the input gateway key is incorrect.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-138">The content or format of the input gateway key is incorrect.</span></span> <span data-ttu-id="b4ad7-139">One of the reasons can be that you copied only a portion of the key from the portal or you're using an invalid key.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-139">One of the reasons can be that you copied only a portion of the key from the portal or you're using an invalid key.</span></span>

#### <a name="resolution"></a><span data-ttu-id="b4ad7-140">Resolution</span><span class="sxs-lookup"><span data-stu-id="b4ad7-140">Resolution</span></span>
<span data-ttu-id="b4ad7-141">Generate a gateway key in the portal, and use the copy button to copy the whole key.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-141">Generate a gateway key in the portal, and use the copy button to copy the whole key.</span></span> <span data-ttu-id="b4ad7-142">Then paste it in this window to register the gateway.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-142">Then paste it in this window to register the gateway.</span></span>

### <a name="5-problem"></a><span data-ttu-id="b4ad7-143">5. Problem</span><span class="sxs-lookup"><span data-stu-id="b4ad7-143">5. Problem</span></span>
<span data-ttu-id="b4ad7-144">You might see the following error message when you're registering a gateway.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-144">You might see the following error message when you're registering a gateway.</span></span>

`Error: The gateway key is invalid or empty. Specify a valid gateway key from the portal.`

![Gateway key is invalid or empty](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a><span data-ttu-id="b4ad7-146">Cause</span><span class="sxs-lookup"><span data-stu-id="b4ad7-146">Cause</span></span>
<span data-ttu-id="b4ad7-147">The gateway key has been regenerated or the gateway has been deleted in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-147">The gateway key has been regenerated or the gateway has been deleted in the Azure portal.</span></span> <span data-ttu-id="b4ad7-148">It can also happen if the Data Management Gateway setup is not latest.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-148">It can also happen if the Data Management Gateway setup is not latest.</span></span>

#### <a name="resolution"></a><span data-ttu-id="b4ad7-149">Resolution</span><span class="sxs-lookup"><span data-stu-id="b4ad7-149">Resolution</span></span>
<span data-ttu-id="b4ad7-150">Check if the Data Management Gateway setup is the latest version, you can find the latest version on the Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span><span class="sxs-lookup"><span data-stu-id="b4ad7-150">Check if the Data Management Gateway setup is the latest version, you can find the latest version on the Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span></span>

<span data-ttu-id="b4ad7-151">If setup is current/ latest and gateway still exists on Portal, regenerate the gateway key in the Azure portal, and use the copy button to copy the whole key, and then paste it in this window to register the gateway.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-151">If setup is current/ latest and gateway still exists on Portal, regenerate the gateway key in the Azure portal, and use the copy button to copy the whole key, and then paste it in this window to register the gateway.</span></span> <span data-ttu-id="b4ad7-152">Otherwise, recreate the gateway and start over.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-152">Otherwise, recreate the gateway and start over.</span></span>

### <a name="6-problem"></a><span data-ttu-id="b4ad7-153">6. Problem</span><span class="sxs-lookup"><span data-stu-id="b4ad7-153">6. Problem</span></span>
<span data-ttu-id="b4ad7-154">You might see the following error message when you're registering a gateway.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-154">You might see the following error message when you're registering a gateway.</span></span>

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with the status “Gateway key is invalid”`

![Gateway key is invalid or empty](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a><span data-ttu-id="b4ad7-156">Cause</span><span class="sxs-lookup"><span data-stu-id="b4ad7-156">Cause</span></span>
<span data-ttu-id="b4ad7-157">This error might happen because either the gateway has been deleted or the associated gateway key has been regenerated.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-157">This error might happen because either the gateway has been deleted or the associated gateway key has been regenerated.</span></span>

#### <a name="resolution"></a><span data-ttu-id="b4ad7-158">Resolution</span><span class="sxs-lookup"><span data-stu-id="b4ad7-158">Resolution</span></span>
<span data-ttu-id="b4ad7-159">If the gateway has been deleted, re-create the gateway from the portal, click **Register**, copy the key from the portal, paste it, and try to register the gateway.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-159">If the gateway has been deleted, re-create the gateway from the portal, click **Register**, copy the key from the portal, paste it, and try to register the gateway.</span></span>

<span data-ttu-id="b4ad7-160">If the gateway still exists but its key has been regenerated, use the new key to register the gateway.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-160">If the gateway still exists but its key has been regenerated, use the new key to register the gateway.</span></span> <span data-ttu-id="b4ad7-161">If you don’t have the key, regenerate the key again from the portal.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-161">If you don’t have the key, regenerate the key again from the portal.</span></span>

### <a name="7-problem"></a><span data-ttu-id="b4ad7-162">7. Problem</span><span class="sxs-lookup"><span data-stu-id="b4ad7-162">7. Problem</span></span>
<span data-ttu-id="b4ad7-163">When you're registering a gateway, you might need to enter path and password for a certificate.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-163">When you're registering a gateway, you might need to enter path and password for a certificate.</span></span>

![Specify certificate](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a><span data-ttu-id="b4ad7-165">Cause</span><span class="sxs-lookup"><span data-stu-id="b4ad7-165">Cause</span></span>
<span data-ttu-id="b4ad7-166">The gateway has been registered on other machines before.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-166">The gateway has been registered on other machines before.</span></span> <span data-ttu-id="b4ad7-167">During the initial registration of a gateway, an encryption certificate has been associated with the gateway.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-167">During the initial registration of a gateway, an encryption certificate has been associated with the gateway.</span></span> <span data-ttu-id="b4ad7-168">The certificate can either be self-generated by the gateway or provided by the user.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-168">The certificate can either be self-generated by the gateway or provided by the user.</span></span>  <span data-ttu-id="b4ad7-169">This certificate is used to encrypt credentials of the data store (linked service).</span><span class="sxs-lookup"><span data-stu-id="b4ad7-169">This certificate is used to encrypt credentials of the data store (linked service).</span></span>  

![Export certificate](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

<span data-ttu-id="b4ad7-171">When restoring the gateway on a different host machine, the registration wizard asks for this certificate to decrypt credentials previously encrypted with this certificate.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-171">When restoring the gateway on a different host machine, the registration wizard asks for this certificate to decrypt credentials previously encrypted with this certificate.</span></span>  <span data-ttu-id="b4ad7-172">Without this certificate, the credentials cannot be decrypted by the new gateway and subsequent copy activity executions associated with this new gateway will fail.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-172">Without this certificate, the credentials cannot be decrypted by the new gateway and subsequent copy activity executions associated with this new gateway will fail.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="b4ad7-173">Resolution</span><span class="sxs-lookup"><span data-stu-id="b4ad7-173">Resolution</span></span>
<span data-ttu-id="b4ad7-174">If you have exported the credential certificate from the original gateway machine by using the **Export** button on the **Settings** tab in Data Management Gateway Configuration Manager, use the certificate here.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-174">If you have exported the credential certificate from the original gateway machine by using the **Export** button on the **Settings** tab in Data Management Gateway Configuration Manager, use the certificate here.</span></span>

<span data-ttu-id="b4ad7-175">You cannot skip this stage when recovering a gateway.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-175">You cannot skip this stage when recovering a gateway.</span></span> <span data-ttu-id="b4ad7-176">If the certificate is missing, you need to delete the gateway from the portal and re-create a new gateway.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-176">If the certificate is missing, you need to delete the gateway from the portal and re-create a new gateway.</span></span>  <span data-ttu-id="b4ad7-177">In addition, update all linked services that are related to the gateway by reentering their credentials.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-177">In addition, update all linked services that are related to the gateway by reentering their credentials.</span></span>

### <a name="8-problem"></a><span data-ttu-id="b4ad7-178">8. Problem</span><span class="sxs-lookup"><span data-stu-id="b4ad7-178">8. Problem</span></span>
<span data-ttu-id="b4ad7-179">You might see the following error message.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-179">You might see the following error message.</span></span>

`Error: The remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a><span data-ttu-id="b4ad7-180">Cause</span><span class="sxs-lookup"><span data-stu-id="b4ad7-180">Cause</span></span>
<span data-ttu-id="b4ad7-181">This error happens when your gateway is in an environment that requires an HTTP proxy to access Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-181">This error happens when your gateway is in an environment that requires an HTTP proxy to access Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span></span>

#### <a name="resolution"></a><span data-ttu-id="b4ad7-182">Resolution</span><span class="sxs-lookup"><span data-stu-id="b4ad7-182">Resolution</span></span>
<span data-ttu-id="b4ad7-183">Follow the instructions in the [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-183">Follow the instructions in the [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span></span>

## <a name="gateway-is-online-with-limited-functionality"></a><span data-ttu-id="b4ad7-184">Gateway is online with limited functionality</span><span class="sxs-lookup"><span data-stu-id="b4ad7-184">Gateway is online with limited functionality</span></span>
### <a name="1-problem"></a><span data-ttu-id="b4ad7-185">1. Problem</span><span class="sxs-lookup"><span data-stu-id="b4ad7-185">1. Problem</span></span>
<span data-ttu-id="b4ad7-186">You see the status of the gateway as online with limited functionality.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-186">You see the status of the gateway as online with limited functionality.</span></span>

#### <a name="cause"></a><span data-ttu-id="b4ad7-187">Cause</span><span class="sxs-lookup"><span data-stu-id="b4ad7-187">Cause</span></span>
<span data-ttu-id="b4ad7-188">You see the status of the gateway as online with limited functionality for one of the following reasons:</span><span class="sxs-lookup"><span data-stu-id="b4ad7-188">You see the status of the gateway as online with limited functionality for one of the following reasons:</span></span>

* <span data-ttu-id="b4ad7-189">Gateway cannot connect to cloud service through Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-189">Gateway cannot connect to cloud service through Azure Service Bus.</span></span>
* <span data-ttu-id="b4ad7-190">Cloud service cannot connect to gateway through Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-190">Cloud service cannot connect to gateway through Service Bus.</span></span>

<span data-ttu-id="b4ad7-191">When the gateway is online with limited functionality, you might not be able to use the Data Factory Copy Wizard to create data pipelines for copying data to or from on-premises data stores.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-191">When the gateway is online with limited functionality, you might not be able to use the Data Factory Copy Wizard to create data pipelines for copying data to or from on-premises data stores.</span></span> <span data-ttu-id="b4ad7-192">As a workaround, you can use Data Factory Editor in the portal, Visual Studio, or Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-192">As a workaround, you can use Data Factory Editor in the portal, Visual Studio, or Azure PowerShell.</span></span>

#### <a name="resolution"></a><span data-ttu-id="b4ad7-193">Resolution</span><span class="sxs-lookup"><span data-stu-id="b4ad7-193">Resolution</span></span>
<span data-ttu-id="b4ad7-194">Resolution for this issue (online with limited functionality) is based on whether the gateway cannot connect to the cloud service or the other way.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-194">Resolution for this issue (online with limited functionality) is based on whether the gateway cannot connect to the cloud service or the other way.</span></span> <span data-ttu-id="b4ad7-195">The following sections provide these resolutions.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-195">The following sections provide these resolutions.</span></span>

### <a name="2-problem"></a><span data-ttu-id="b4ad7-196">2. Problem</span><span class="sxs-lookup"><span data-stu-id="b4ad7-196">2. Problem</span></span>
<span data-ttu-id="b4ad7-197">You see the following error.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-197">You see the following error.</span></span>

`Error: Gateway cannot connect to cloud service through service bus`

![Gateway cannot connect to cloud service](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a><span data-ttu-id="b4ad7-199">Cause</span><span class="sxs-lookup"><span data-stu-id="b4ad7-199">Cause</span></span>
<span data-ttu-id="b4ad7-200">Gateway cannot connect to the cloud service through Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-200">Gateway cannot connect to the cloud service through Service Bus.</span></span>

#### <a name="resolution"></a><span data-ttu-id="b4ad7-201">Resolution</span><span class="sxs-lookup"><span data-stu-id="b4ad7-201">Resolution</span></span>
<span data-ttu-id="b4ad7-202">Follow these steps to get the gateway back online:</span><span class="sxs-lookup"><span data-stu-id="b4ad7-202">Follow these steps to get the gateway back online:</span></span>

1. <span data-ttu-id="b4ad7-203">Allow IP address outbound rules on the gateway machine and the corporate firewall.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-203">Allow IP address outbound rules on the gateway machine and the corporate firewall.</span></span> <span data-ttu-id="b4ad7-204">You can find IP addresses from the Windows Event Log (ID == 401): An attempt was made to access a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-204">You can find IP addresses from the Windows Event Log (ID == 401): An attempt was made to access a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span></span>
* <span data-ttu-id="b4ad7-205">Configure proxy settings on the gateway.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-205">Configure proxy settings on the gateway.</span></span> <span data-ttu-id="b4ad7-206">See the [Proxy server considerations](#proxy-server-considerations) section for details.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-206">See the [Proxy server considerations](#proxy-server-considerations) section for details.</span></span>
* <span data-ttu-id="b4ad7-207">Enable outbound ports 5671 and 9350-9354 on both the Windows Firewall on the gateway machine and the corporate firewall.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-207">Enable outbound ports 5671 and 9350-9354 on both the Windows Firewall on the gateway machine and the corporate firewall.</span></span> <span data-ttu-id="b4ad7-208">See the [Ports and firewall](#ports-and-firewall) section for details.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-208">See the [Ports and firewall](#ports-and-firewall) section for details.</span></span> <span data-ttu-id="b4ad7-209">This step is optional, but we recommend it for performance consideration.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-209">This step is optional, but we recommend it for performance consideration.</span></span>

### <a name="3-problem"></a><span data-ttu-id="b4ad7-210">3. Problem</span><span class="sxs-lookup"><span data-stu-id="b4ad7-210">3. Problem</span></span>
<span data-ttu-id="b4ad7-211">You see the following error.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-211">You see the following error.</span></span>

`Error: Cloud service cannot connect to gateway through service bus.`

#### <a name="cause"></a><span data-ttu-id="b4ad7-212">Cause</span><span class="sxs-lookup"><span data-stu-id="b4ad7-212">Cause</span></span>
<span data-ttu-id="b4ad7-213">A transient error in network connectivity.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-213">A transient error in network connectivity.</span></span>

#### <a name="resolution"></a><span data-ttu-id="b4ad7-214">Resolution</span><span class="sxs-lookup"><span data-stu-id="b4ad7-214">Resolution</span></span>
<span data-ttu-id="b4ad7-215">Follow these steps to get the gateway back online:</span><span class="sxs-lookup"><span data-stu-id="b4ad7-215">Follow these steps to get the gateway back online:</span></span>

1. <span data-ttu-id="b4ad7-216">Wait for a couple of minutes, the connectivity will be automatically recovered when the error is gone.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-216">Wait for a couple of minutes, the connectivity will be automatically recovered when the error is gone.</span></span>
* <span data-ttu-id="b4ad7-217">If the error persists, restart the gateway service.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-217">If the error persists, restart the gateway service.</span></span>

## <a name="failed-to-author-linked-service"></a><span data-ttu-id="b4ad7-218">Failed to author linked service</span><span class="sxs-lookup"><span data-stu-id="b4ad7-218">Failed to author linked service</span></span>
### <a name="problem"></a><span data-ttu-id="b4ad7-219">Problem</span><span class="sxs-lookup"><span data-stu-id="b4ad7-219">Problem</span></span>
<span data-ttu-id="b4ad7-220">You might see this error when you try to use Credential Manager in the portal to input credentials for a new linked service, or update credentials for an existing linked service.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-220">You might see this error when you try to use Credential Manager in the portal to input credentials for a new linked service, or update credentials for an existing linked service.</span></span>

`Error: The data store '<Server>/<Database>' cannot be reached. Check connection settings for the data source.`

<span data-ttu-id="b4ad7-221">When you see this error, the settings page of Data Management Gateway Configuration Manager might look like the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-221">When you see this error, the settings page of Data Management Gateway Configuration Manager might look like the following screenshot.</span></span>

![Database cannot be reached](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a><span data-ttu-id="b4ad7-223">Cause</span><span class="sxs-lookup"><span data-stu-id="b4ad7-223">Cause</span></span>
<span data-ttu-id="b4ad7-224">The SSL certificate might have been lost on the gateway machine.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-224">The SSL certificate might have been lost on the gateway machine.</span></span> <span data-ttu-id="b4ad7-225">The gateway computer cannot load the certificate currently that is used for SSL encryption.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-225">The gateway computer cannot load the certificate currently that is used for SSL encryption.</span></span> <span data-ttu-id="b4ad7-226">You might also see an error message in the event log that is similar to the following message.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-226">You might also see an error message in the event log that is similar to the following message.</span></span>

 `Unable to get the gateway settings from cloud service. Check the gateway key and the network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a><span data-ttu-id="b4ad7-227">Resolution</span><span class="sxs-lookup"><span data-stu-id="b4ad7-227">Resolution</span></span>
<span data-ttu-id="b4ad7-228">Follow these steps to solve the problem:</span><span class="sxs-lookup"><span data-stu-id="b4ad7-228">Follow these steps to solve the problem:</span></span>

1. <span data-ttu-id="b4ad7-229">Start Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-229">Start Data Management Gateway Configuration Manager.</span></span>
2. <span data-ttu-id="b4ad7-230">Switch to the **Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-230">Switch to the **Settings** tab.</span></span>  
3. <span data-ttu-id="b4ad7-231">Click the **Change** button to change the SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-231">Click the **Change** button to change the SSL certificate.</span></span>

   ![Change certificate button](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. <span data-ttu-id="b4ad7-233">Select a new certificate as the SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-233">Select a new certificate as the SSL certificate.</span></span> <span data-ttu-id="b4ad7-234">You can use any SSL certificate that is generated by you or any organization.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-234">You can use any SSL certificate that is generated by you or any organization.</span></span>

   ![Specify certificate](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a><span data-ttu-id="b4ad7-236">Copy activity fails</span><span class="sxs-lookup"><span data-stu-id="b4ad7-236">Copy activity fails</span></span>
### <a name="problem"></a><span data-ttu-id="b4ad7-237">Problem</span><span class="sxs-lookup"><span data-stu-id="b4ad7-237">Problem</span></span>
<span data-ttu-id="b4ad7-238">You might notice the following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in the portal.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-238">You might notice the following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in the portal.</span></span>

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect to SQL Server`

#### <a name="cause"></a><span data-ttu-id="b4ad7-239">Cause</span><span class="sxs-lookup"><span data-stu-id="b4ad7-239">Cause</span></span>
<span data-ttu-id="b4ad7-240">This can happen for different reasons, and mitigation varies accordingly.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-240">This can happen for different reasons, and mitigation varies accordingly.</span></span>

#### <a name="resolution"></a><span data-ttu-id="b4ad7-241">Resolution</span><span class="sxs-lookup"><span data-stu-id="b4ad7-241">Resolution</span></span>
<span data-ttu-id="b4ad7-242">Allow outbound TCP connections over port TCP/1433 on the Data Management Gateway client side before connecting to an SQL database.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-242">Allow outbound TCP connections over port TCP/1433 on the Data Management Gateway client side before connecting to an SQL database.</span></span>

<span data-ttu-id="b4ad7-243">If the target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-243">If the target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span></span>

<span data-ttu-id="b4ad7-244">See the following section to test the connection to the on-premises data store.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-244">See the following section to test the connection to the on-premises data store.</span></span>

## <a name="data-store-connection-or-driver-related-errors"></a><span data-ttu-id="b4ad7-245">Data store connection or driver-related errors</span><span class="sxs-lookup"><span data-stu-id="b4ad7-245">Data store connection or driver-related errors</span></span>
<span data-ttu-id="b4ad7-246">If you see data store connection or driver-related errors, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="b4ad7-246">If you see data store connection or driver-related errors, complete the following steps:</span></span>

1. <span data-ttu-id="b4ad7-247">Start Data Management Gateway Configuration Manager on the gateway machine.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-247">Start Data Management Gateway Configuration Manager on the gateway machine.</span></span>
2. <span data-ttu-id="b4ad7-248">Switch to the **Diagnostics** tab.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-248">Switch to the **Diagnostics** tab.</span></span>
3. <span data-ttu-id="b4ad7-249">In **Test Connection**, add the gateway group values.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-249">In **Test Connection**, add the gateway group values.</span></span>
4. <span data-ttu-id="b4ad7-250">Click **Test** to see if you can connect to the on-premises data source from the gateway machine by using the connection information and credentials.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-250">Click **Test** to see if you can connect to the on-premises data source from the gateway machine by using the connection information and credentials.</span></span> <span data-ttu-id="b4ad7-251">If the test connection still fails after you install a driver, restart the gateway for it to pick up the latest change.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-251">If the test connection still fails after you install a driver, restart the gateway for it to pick up the latest change.</span></span>

![Test Connection in Diagnostics tab](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a><span data-ttu-id="b4ad7-253">Gateway logs</span><span class="sxs-lookup"><span data-stu-id="b4ad7-253">Gateway logs</span></span>
### <a name="send-gateway-logs-to-microsoft"></a><span data-ttu-id="b4ad7-254">Send gateway logs to Microsoft</span><span class="sxs-lookup"><span data-stu-id="b4ad7-254">Send gateway logs to Microsoft</span></span>
<span data-ttu-id="b4ad7-255">When you contact Microsoft Support to get help with troubleshooting gateway issues, you might be asked to share your gateway logs.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-255">When you contact Microsoft Support to get help with troubleshooting gateway issues, you might be asked to share your gateway logs.</span></span> <span data-ttu-id="b4ad7-256">With the release of the gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-256">With the release of the gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span></span>    

1. <span data-ttu-id="b4ad7-257">Switch to the **Diagnostics** tab in Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-257">Switch to the **Diagnostics** tab in Data Management Gateway Configuration Manager.</span></span>

    ![Data Management Gateway Diagnostics tab](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. <span data-ttu-id="b4ad7-259">Click **Send Logs** to see the following dialog box.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-259">Click **Send Logs** to see the following dialog box.</span></span>

    ![Data Management Gateway Send logs](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. <span data-ttu-id="b4ad7-261">(Optional) Click **view logs** to review logs in the event viewer.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-261">(Optional) Click **view logs** to review logs in the event viewer.</span></span>
4. <span data-ttu-id="b4ad7-262">(Optional) Click **privacy** to review Microsoft web services privacy statement.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-262">(Optional) Click **privacy** to review Microsoft web services privacy statement.</span></span>
5. <span data-ttu-id="b4ad7-263">When you are satisfied with what you are about to upload, click **Send Logs** to actually send the logs from the last seven days to Microsoft for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-263">When you are satisfied with what you are about to upload, click **Send Logs** to actually send the logs from the last seven days to Microsoft for troubleshooting.</span></span> <span data-ttu-id="b4ad7-264">You should see the status of the send-logs operation as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-264">You should see the status of the send-logs operation as shown in the following screenshot.</span></span>

    ![Data Management Gateway Send logs status](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. <span data-ttu-id="b4ad7-266">After the operation is complete, you see a dialog box as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-266">After the operation is complete, you see a dialog box as shown in the following screenshot.</span></span>

    ![Data Management Gateway Send logs status](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. <span data-ttu-id="b4ad7-268">Save the **Report ID** and share it with Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-268">Save the **Report ID** and share it with Microsoft Support.</span></span> <span data-ttu-id="b4ad7-269">The report ID is used to locate the gateway logs that you uploaded for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-269">The report ID is used to locate the gateway logs that you uploaded for troubleshooting.</span></span>  <span data-ttu-id="b4ad7-270">The report ID is also saved in the event viewer.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-270">The report ID is also saved in the event viewer.</span></span>  <span data-ttu-id="b4ad7-271">You can find it by looking at the event ID “25”, and check the date and time.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-271">You can find it by looking at the event ID “25”, and check the date and time.</span></span>

    ![Data Management Gateway Send logs report ID](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a><span data-ttu-id="b4ad7-273">Archive gateway logs on gateway host machine</span><span class="sxs-lookup"><span data-stu-id="b4ad7-273">Archive gateway logs on gateway host machine</span></span>
<span data-ttu-id="b4ad7-274">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span><span class="sxs-lookup"><span data-stu-id="b4ad7-274">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span></span>

* <span data-ttu-id="b4ad7-275">You manually install the gateway and register the gateway.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-275">You manually install the gateway and register the gateway.</span></span>
* <span data-ttu-id="b4ad7-276">You try to register the gateway with a regenerated key in Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-276">You try to register the gateway with a regenerated key in Data Management Gateway Configuration Manager.</span></span>
* <span data-ttu-id="b4ad7-277">You try to send logs and the gateway host service cannot be connected.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-277">You try to send logs and the gateway host service cannot be connected.</span></span>

<span data-ttu-id="b4ad7-278">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-278">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span></span> <span data-ttu-id="b4ad7-279">For example, if you receive an error while you register the gateway as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-279">For example, if you receive an error while you register the gateway as shown in the following screenshot.</span></span>   

![Data Management Gateway Registration error](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

<span data-ttu-id="b4ad7-281">Click the **Archive gateway logs** link to archive and save logs, and then share the zip file with Microsoft support.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-281">Click the **Archive gateway logs** link to archive and save logs, and then share the zip file with Microsoft support.</span></span>

![Data Management Gateway Archive logs](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a><span data-ttu-id="b4ad7-283">Locate gateway logs</span><span class="sxs-lookup"><span data-stu-id="b4ad7-283">Locate gateway logs</span></span>
<span data-ttu-id="b4ad7-284">You can find detailed gateway log information in the Windows event logs.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-284">You can find detailed gateway log information in the Windows event logs.</span></span>

1. <span data-ttu-id="b4ad7-285">Start Windows **Event Viewer**.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-285">Start Windows **Event Viewer**.</span></span>
2. <span data-ttu-id="b4ad7-286">Locate logs in the **Application and Services Logs** > **Data Management Gateway** folder.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-286">Locate logs in the **Application and Services Logs** > **Data Management Gateway** folder.</span></span>

 <span data-ttu-id="b4ad7-287">When you're troubleshooting gateway-related issues, look for error level events in the event viewer.</span><span class="sxs-lookup"><span data-stu-id="b4ad7-287">When you're troubleshooting gateway-related issues, look for error level events in the event viewer.</span></span>

![Data Management Gateway logs in event viewer](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
