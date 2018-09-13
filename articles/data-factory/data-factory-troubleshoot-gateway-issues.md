---
title: Troubleshoot Data Management Gateway issues | Microsoft Docs
description: Provides tips to troubleshoot issues related to Data Management Gateway.
services: data-factory
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/25/2017
ms.author: jingwang
published: true
ms.openlocfilehash: 5f745e0dc639c0986af87b0fc064086f9a405840
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552154"
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a><span data-ttu-id="bda95-103">Troubleshoot issues with using Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="bda95-103">Troubleshoot issues with using Data Management Gateway</span></span>
<span data-ttu-id="bda95-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="bda95-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="bda95-105">See the [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about the gateway.</span><span class="sxs-lookup"><span data-stu-id="bda95-105">See the [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about the gateway.</span></span> <span data-ttu-id="bda95-106">See the [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database to Microsoft Azure Blob storage by using the gateway.</span><span class="sxs-lookup"><span data-stu-id="bda95-106">See the [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database to Microsoft Azure Blob storage by using the gateway.</span></span>
>
>

## <a name="failed-to-install-or-register-gateway"></a><span data-ttu-id="bda95-107">Failed to install or register gateway</span><span class="sxs-lookup"><span data-stu-id="bda95-107">Failed to install or register gateway</span></span>
### <a name="1-problem"></a><span data-ttu-id="bda95-108">1. Problem</span><span class="sxs-lookup"><span data-stu-id="bda95-108">1. Problem</span></span>
<span data-ttu-id="bda95-109">You see this error message when installing and registering a gateway, specifically, while downloading the gateway installation file.</span><span class="sxs-lookup"><span data-stu-id="bda95-109">You see this error message when installing and registering a gateway, specifically, while downloading the gateway installation file.</span></span>

`Unable to connect to the remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a><span data-ttu-id="bda95-110">Cause</span><span class="sxs-lookup"><span data-stu-id="bda95-110">Cause</span></span>
<span data-ttu-id="bda95-111">The machine on which you are trying to install the gateway has failed to download the latest gateway installation file from the download center due to a network issue.</span><span class="sxs-lookup"><span data-stu-id="bda95-111">The machine on which you are trying to install the gateway has failed to download the latest gateway installation file from the download center due to a network issue.</span></span>

#### <a name="resolution"></a><span data-ttu-id="bda95-112">Resolution</span><span class="sxs-lookup"><span data-stu-id="bda95-112">Resolution</span></span>
<span data-ttu-id="bda95-113">Check your firewall proxy server settings to see whether the settings block the network connection from the computer to the [download center](https://download.microsoft.com/), and update the settings accordingly.</span><span class="sxs-lookup"><span data-stu-id="bda95-113">Check your firewall proxy server settings to see whether the settings block the network connection from the computer to the [download center](https://download.microsoft.com/), and update the settings accordingly.</span></span>

<span data-ttu-id="bda95-114">Alternatively, you can download the installation file for the latest gateway from the [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access the download center.</span><span class="sxs-lookup"><span data-stu-id="bda95-114">Alternatively, you can download the installation file for the latest gateway from the [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access the download center.</span></span> <span data-ttu-id="bda95-115">You can then copy the installer file to the gateway host computer and run it manually to install and update the gateway.</span><span class="sxs-lookup"><span data-stu-id="bda95-115">You can then copy the installer file to the gateway host computer and run it manually to install and update the gateway.</span></span>

### <a name="2-problem"></a><span data-ttu-id="bda95-116">2. Problem</span><span class="sxs-lookup"><span data-stu-id="bda95-116">2. Problem</span></span>
<span data-ttu-id="bda95-117">You see this error when you're attempting to install a gateway by clicking **install directly on this computer** in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bda95-117">You see this error when you're attempting to install a gateway by clicking **install directly on this computer** in the Azure portal.</span></span>

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a><span data-ttu-id="bda95-118">Cause</span><span class="sxs-lookup"><span data-stu-id="bda95-118">Cause</span></span>
<span data-ttu-id="bda95-119">A gateway is already installed on the machine.</span><span class="sxs-lookup"><span data-stu-id="bda95-119">A gateway is already installed on the machine.</span></span>

#### <a name="resolution"></a><span data-ttu-id="bda95-120">Resolution</span><span class="sxs-lookup"><span data-stu-id="bda95-120">Resolution</span></span>
<span data-ttu-id="bda95-121">Uninstall the existing gateway on the machine and click the **install directly on this computer** link again.</span><span class="sxs-lookup"><span data-stu-id="bda95-121">Uninstall the existing gateway on the machine and click the **install directly on this computer** link again.</span></span>

### <a name="3-problem"></a><span data-ttu-id="bda95-122">3. Problem</span><span class="sxs-lookup"><span data-stu-id="bda95-122">3. Problem</span></span>
<span data-ttu-id="bda95-123">You might see this error when registering a new gateway.</span><span class="sxs-lookup"><span data-stu-id="bda95-123">You might see this error when registering a new gateway.</span></span>

`Error: The gateway has encountered an error during registration.`

#### <a name="cause"></a><span data-ttu-id="bda95-124">Cause</span><span class="sxs-lookup"><span data-stu-id="bda95-124">Cause</span></span>
<span data-ttu-id="bda95-125">You might see this message for one of the following reasons:</span><span class="sxs-lookup"><span data-stu-id="bda95-125">You might see this message for one of the following reasons:</span></span>

* <span data-ttu-id="bda95-126">The format of the gateway key is invalid.</span><span class="sxs-lookup"><span data-stu-id="bda95-126">The format of the gateway key is invalid.</span></span>
* <span data-ttu-id="bda95-127">The gateway key has been invalidated.</span><span class="sxs-lookup"><span data-stu-id="bda95-127">The gateway key has been invalidated.</span></span>
* <span data-ttu-id="bda95-128">The gateway key has been regenerated from the portal.</span><span class="sxs-lookup"><span data-stu-id="bda95-128">The gateway key has been regenerated from the portal.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="bda95-129">Resolution</span><span class="sxs-lookup"><span data-stu-id="bda95-129">Resolution</span></span>
<span data-ttu-id="bda95-130">Verify whether you are using the right gateway key from the portal.</span><span class="sxs-lookup"><span data-stu-id="bda95-130">Verify whether you are using the right gateway key from the portal.</span></span> <span data-ttu-id="bda95-131">If needed, regenerate a key and use the key to register the gateway.</span><span class="sxs-lookup"><span data-stu-id="bda95-131">If needed, regenerate a key and use the key to register the gateway.</span></span>

### <a name="4-problem"></a><span data-ttu-id="bda95-132">4. Problem</span><span class="sxs-lookup"><span data-stu-id="bda95-132">4. Problem</span></span>
<span data-ttu-id="bda95-133">You might see the following error message when you're registering a gateway.</span><span class="sxs-lookup"><span data-stu-id="bda95-133">You might see the following error message when you're registering a gateway.</span></span>

`Error: The content or format of the gateway key "{gatewayKey}" is invalid, please go to azure portal to create one new gateway or regenerate the gateway key.`



![Content or format of key is invalid](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a><span data-ttu-id="bda95-135">Cause</span><span class="sxs-lookup"><span data-stu-id="bda95-135">Cause</span></span>
<span data-ttu-id="bda95-136">The content or format of the input gateway key is incorrect.</span><span class="sxs-lookup"><span data-stu-id="bda95-136">The content or format of the input gateway key is incorrect.</span></span> <span data-ttu-id="bda95-137">One of the reasons can be that you copied only a portion of the key from the portal or you're using an invalid key.</span><span class="sxs-lookup"><span data-stu-id="bda95-137">One of the reasons can be that you copied only a portion of the key from the portal or you're using an invalid key.</span></span>

#### <a name="resolution"></a><span data-ttu-id="bda95-138">Resolution</span><span class="sxs-lookup"><span data-stu-id="bda95-138">Resolution</span></span>
<span data-ttu-id="bda95-139">Generate a gateway key in the portal, and use the copy button to copy the whole key.</span><span class="sxs-lookup"><span data-stu-id="bda95-139">Generate a gateway key in the portal, and use the copy button to copy the whole key.</span></span> <span data-ttu-id="bda95-140">Then paste it in this window to register the gateway.</span><span class="sxs-lookup"><span data-stu-id="bda95-140">Then paste it in this window to register the gateway.</span></span>

### <a name="5-problem"></a><span data-ttu-id="bda95-141">5. Problem</span><span class="sxs-lookup"><span data-stu-id="bda95-141">5. Problem</span></span>
<span data-ttu-id="bda95-142">You might see the following error message when you're registering a gateway.</span><span class="sxs-lookup"><span data-stu-id="bda95-142">You might see the following error message when you're registering a gateway.</span></span>

`Error: The gateway key is invalid or empty. Specify a valid gateway key from the portal.`

![Gateway key is invalid or empty](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a><span data-ttu-id="bda95-144">Cause</span><span class="sxs-lookup"><span data-stu-id="bda95-144">Cause</span></span>
<span data-ttu-id="bda95-145">The gateway key has been regenerated or the gateway has been deleted in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bda95-145">The gateway key has been regenerated or the gateway has been deleted in the Azure portal.</span></span> <span data-ttu-id="bda95-146">It can also happen if the Data Management Gateway setup is not latest.</span><span class="sxs-lookup"><span data-stu-id="bda95-146">It can also happen if the Data Management Gateway setup is not latest.</span></span>

#### <a name="resolution"></a><span data-ttu-id="bda95-147">Resolution</span><span class="sxs-lookup"><span data-stu-id="bda95-147">Resolution</span></span>
<span data-ttu-id="bda95-148">Check if the Data Management Gateway setup is the latest version, you can find the latest version on the Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span><span class="sxs-lookup"><span data-stu-id="bda95-148">Check if the Data Management Gateway setup is the latest version, you can find the latest version on the Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span></span>

<span data-ttu-id="bda95-149">If setup is current/ latest and gateway still exists on Portal, regenerate the gateway key in the Azure portal, and use the copy button to copy the whole key, and then paste it in this window to register the gateway.</span><span class="sxs-lookup"><span data-stu-id="bda95-149">If setup is current/ latest and gateway still exists on Portal, regenerate the gateway key in the Azure portal, and use the copy button to copy the whole key, and then paste it in this window to register the gateway.</span></span> <span data-ttu-id="bda95-150">Otherwise, recreate the gateway and start over.</span><span class="sxs-lookup"><span data-stu-id="bda95-150">Otherwise, recreate the gateway and start over.</span></span>

### <a name="6-problem"></a><span data-ttu-id="bda95-151">6. Problem</span><span class="sxs-lookup"><span data-stu-id="bda95-151">6. Problem</span></span>
<span data-ttu-id="bda95-152">You might see the following error message when you're registering a gateway.</span><span class="sxs-lookup"><span data-stu-id="bda95-152">You might see the following error message when you're registering a gateway.</span></span>

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with the status “Gateway key is invalid”`

![Gateway key is invalid or empty](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a><span data-ttu-id="bda95-154">Cause</span><span class="sxs-lookup"><span data-stu-id="bda95-154">Cause</span></span>
<span data-ttu-id="bda95-155">This error might happen because either the gateway has been deleted or the associated gateway key has been regenerated.</span><span class="sxs-lookup"><span data-stu-id="bda95-155">This error might happen because either the gateway has been deleted or the associated gateway key has been regenerated.</span></span>

#### <a name="resolution"></a><span data-ttu-id="bda95-156">Resolution</span><span class="sxs-lookup"><span data-stu-id="bda95-156">Resolution</span></span>
<span data-ttu-id="bda95-157">If the gateway has been deleted, re-create the gateway from the portal, click **Register**, copy the key from the portal, paste it, and try to register the gateway.</span><span class="sxs-lookup"><span data-stu-id="bda95-157">If the gateway has been deleted, re-create the gateway from the portal, click **Register**, copy the key from the portal, paste it, and try to register the gateway.</span></span>

<span data-ttu-id="bda95-158">If the gateway still exists but its key has been regenerated, use the new key to register the gateway.</span><span class="sxs-lookup"><span data-stu-id="bda95-158">If the gateway still exists but its key has been regenerated, use the new key to register the gateway.</span></span> <span data-ttu-id="bda95-159">If you don’t have the key, regenerate the key again from the portal.</span><span class="sxs-lookup"><span data-stu-id="bda95-159">If you don’t have the key, regenerate the key again from the portal.</span></span>

### <a name="7-problem"></a><span data-ttu-id="bda95-160">7. Problem</span><span class="sxs-lookup"><span data-stu-id="bda95-160">7. Problem</span></span>
<span data-ttu-id="bda95-161">When you're registering a gateway, you might need to enter path and password for a certificate.</span><span class="sxs-lookup"><span data-stu-id="bda95-161">When you're registering a gateway, you might need to enter path and password for a certificate.</span></span>

![Specify certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a><span data-ttu-id="bda95-163">Cause</span><span class="sxs-lookup"><span data-stu-id="bda95-163">Cause</span></span>
<span data-ttu-id="bda95-164">The gateway has been registered on other machines before.</span><span class="sxs-lookup"><span data-stu-id="bda95-164">The gateway has been registered on other machines before.</span></span> <span data-ttu-id="bda95-165">During the initial registration of a gateway, an encryption certificate has been associated with the gateway.</span><span class="sxs-lookup"><span data-stu-id="bda95-165">During the initial registration of a gateway, an encryption certificate has been associated with the gateway.</span></span> <span data-ttu-id="bda95-166">The certificate can either be self-generated by the gateway or provided by the user.</span><span class="sxs-lookup"><span data-stu-id="bda95-166">The certificate can either be self-generated by the gateway or provided by the user.</span></span>  <span data-ttu-id="bda95-167">This certificate is used to encrypt credentials of the data store (linked service).</span><span class="sxs-lookup"><span data-stu-id="bda95-167">This certificate is used to encrypt credentials of the data store (linked service).</span></span>  

![Export certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

<span data-ttu-id="bda95-169">When restoring the gateway on a different host machine, the registration wizard asks for this certificate to decrypt credentials previously encrypted with this certificate.</span><span class="sxs-lookup"><span data-stu-id="bda95-169">When restoring the gateway on a different host machine, the registration wizard asks for this certificate to decrypt credentials previously encrypted with this certificate.</span></span>  <span data-ttu-id="bda95-170">Without this certificate, the credentials cannot be decrypted by the new gateway and subsequent copy activity executions associated with this new gateway will fail.</span><span class="sxs-lookup"><span data-stu-id="bda95-170">Without this certificate, the credentials cannot be decrypted by the new gateway and subsequent copy activity executions associated with this new gateway will fail.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="bda95-171">Resolution</span><span class="sxs-lookup"><span data-stu-id="bda95-171">Resolution</span></span>
<span data-ttu-id="bda95-172">If you have exported the credential certificate from the original gateway machine by using the **Export** button on the **Settings** tab in Data Management Gateway Configuration Manager, use the certificate here.</span><span class="sxs-lookup"><span data-stu-id="bda95-172">If you have exported the credential certificate from the original gateway machine by using the **Export** button on the **Settings** tab in Data Management Gateway Configuration Manager, use the certificate here.</span></span>

<span data-ttu-id="bda95-173">You cannot skip this stage when recovering a gateway.</span><span class="sxs-lookup"><span data-stu-id="bda95-173">You cannot skip this stage when recovering a gateway.</span></span> <span data-ttu-id="bda95-174">If the certificate is missing, you need to delete the gateway from the portal and re-create a new gateway.</span><span class="sxs-lookup"><span data-stu-id="bda95-174">If the certificate is missing, you need to delete the gateway from the portal and re-create a new gateway.</span></span>  <span data-ttu-id="bda95-175">In addition, update all linked services that are related to the gateway by reentering their credentials.</span><span class="sxs-lookup"><span data-stu-id="bda95-175">In addition, update all linked services that are related to the gateway by reentering their credentials.</span></span>

### <a name="8-problem"></a><span data-ttu-id="bda95-176">8. Problem</span><span class="sxs-lookup"><span data-stu-id="bda95-176">8. Problem</span></span>
<span data-ttu-id="bda95-177">You might see the following error message.</span><span class="sxs-lookup"><span data-stu-id="bda95-177">You might see the following error message.</span></span>

`Error: The remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a><span data-ttu-id="bda95-178">Cause</span><span class="sxs-lookup"><span data-stu-id="bda95-178">Cause</span></span>
<span data-ttu-id="bda95-179">This error happens when your gateway is in an environment that requires an HTTP proxy to access Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span><span class="sxs-lookup"><span data-stu-id="bda95-179">This error happens when your gateway is in an environment that requires an HTTP proxy to access Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span></span>

#### <a name="resolution"></a><span data-ttu-id="bda95-180">Resolution</span><span class="sxs-lookup"><span data-stu-id="bda95-180">Resolution</span></span>
<span data-ttu-id="bda95-181">Follow the instructions in the [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="bda95-181">Follow the instructions in the [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span></span>

## <a name="gateway-is-online-with-limited-functionality"></a><span data-ttu-id="bda95-182">Gateway is online with limited functionality</span><span class="sxs-lookup"><span data-stu-id="bda95-182">Gateway is online with limited functionality</span></span>
### <a name="1-problem"></a><span data-ttu-id="bda95-183">1. Problem</span><span class="sxs-lookup"><span data-stu-id="bda95-183">1. Problem</span></span>
<span data-ttu-id="bda95-184">You see the status of the gateway as online with limited functionality.</span><span class="sxs-lookup"><span data-stu-id="bda95-184">You see the status of the gateway as online with limited functionality.</span></span>

#### <a name="cause"></a><span data-ttu-id="bda95-185">Cause</span><span class="sxs-lookup"><span data-stu-id="bda95-185">Cause</span></span>
<span data-ttu-id="bda95-186">You see the status of the gateway as online with limited functionality for one of the following reasons:</span><span class="sxs-lookup"><span data-stu-id="bda95-186">You see the status of the gateway as online with limited functionality for one of the following reasons:</span></span>

* <span data-ttu-id="bda95-187">Gateway cannot connect to cloud service through Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="bda95-187">Gateway cannot connect to cloud service through Azure Service Bus.</span></span>
* <span data-ttu-id="bda95-188">Cloud service cannot connect to gateway through Service Bus.</span><span class="sxs-lookup"><span data-stu-id="bda95-188">Cloud service cannot connect to gateway through Service Bus.</span></span>

<span data-ttu-id="bda95-189">When the gateway is online with limited functionality, you might not be able to use the Data Factory Copy Wizard to create data pipelines for copying data to or from on-premises data stores.</span><span class="sxs-lookup"><span data-stu-id="bda95-189">When the gateway is online with limited functionality, you might not be able to use the Data Factory Copy Wizard to create data pipelines for copying data to or from on-premises data stores.</span></span> <span data-ttu-id="bda95-190">As a workaround, you can use Data Factory Editor in the portal, Visual Studio, or Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bda95-190">As a workaround, you can use Data Factory Editor in the portal, Visual Studio, or Azure PowerShell.</span></span>

#### <a name="resolution"></a><span data-ttu-id="bda95-191">Resolution</span><span class="sxs-lookup"><span data-stu-id="bda95-191">Resolution</span></span>
<span data-ttu-id="bda95-192">Resolution for this issue (online with limited functionality) is based on whether the gateway cannot connect to the cloud service or the other way.</span><span class="sxs-lookup"><span data-stu-id="bda95-192">Resolution for this issue (online with limited functionality) is based on whether the gateway cannot connect to the cloud service or the other way.</span></span> <span data-ttu-id="bda95-193">The following sections provide these resolutions.</span><span class="sxs-lookup"><span data-stu-id="bda95-193">The following sections provide these resolutions.</span></span>

### <a name="2-problem"></a><span data-ttu-id="bda95-194">2. Problem</span><span class="sxs-lookup"><span data-stu-id="bda95-194">2. Problem</span></span>
<span data-ttu-id="bda95-195">You see the following error.</span><span class="sxs-lookup"><span data-stu-id="bda95-195">You see the following error.</span></span>

`Error: Gateway cannot connect to cloud service through service bus`

![Gateway cannot connect to cloud service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a><span data-ttu-id="bda95-197">Cause</span><span class="sxs-lookup"><span data-stu-id="bda95-197">Cause</span></span>
<span data-ttu-id="bda95-198">Gateway cannot connect to the cloud service through Service Bus.</span><span class="sxs-lookup"><span data-stu-id="bda95-198">Gateway cannot connect to the cloud service through Service Bus.</span></span>

#### <a name="resolution"></a><span data-ttu-id="bda95-199">Resolution</span><span class="sxs-lookup"><span data-stu-id="bda95-199">Resolution</span></span>
<span data-ttu-id="bda95-200">Follow these steps to get the gateway back online:</span><span class="sxs-lookup"><span data-stu-id="bda95-200">Follow these steps to get the gateway back online:</span></span>

1. <span data-ttu-id="bda95-201">Allow IP address outbound rules on the gateway machine and the corporate firewall.</span><span class="sxs-lookup"><span data-stu-id="bda95-201">Allow IP address outbound rules on the gateway machine and the corporate firewall.</span></span> <span data-ttu-id="bda95-202">You can find IP addresses from the Windows Event Log (ID == 401): An attempt was made to access a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span><span class="sxs-lookup"><span data-stu-id="bda95-202">You can find IP addresses from the Windows Event Log (ID == 401): An attempt was made to access a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span></span>
* <span data-ttu-id="bda95-203">Configure proxy settings on the gateway.</span><span class="sxs-lookup"><span data-stu-id="bda95-203">Configure proxy settings on the gateway.</span></span> <span data-ttu-id="bda95-204">See the [Proxy server considerations](#proxy-server-considerations) section for details.</span><span class="sxs-lookup"><span data-stu-id="bda95-204">See the [Proxy server considerations](#proxy-server-considerations) section for details.</span></span>
* <span data-ttu-id="bda95-205">Enable outbound ports 5671 and 9350-9354 on both the Windows Firewall on the gateway machine and the corporate firewall.</span><span class="sxs-lookup"><span data-stu-id="bda95-205">Enable outbound ports 5671 and 9350-9354 on both the Windows Firewall on the gateway machine and the corporate firewall.</span></span> <span data-ttu-id="bda95-206">See the [Ports and firewall](#ports-and-firewall) section for details.</span><span class="sxs-lookup"><span data-stu-id="bda95-206">See the [Ports and firewall](#ports-and-firewall) section for details.</span></span> <span data-ttu-id="bda95-207">This step is optional, but we recommend it for performance consideration.</span><span class="sxs-lookup"><span data-stu-id="bda95-207">This step is optional, but we recommend it for performance consideration.</span></span>

### <a name="3-problem"></a><span data-ttu-id="bda95-208">3. Problem</span><span class="sxs-lookup"><span data-stu-id="bda95-208">3. Problem</span></span>
<span data-ttu-id="bda95-209">You see the following error.</span><span class="sxs-lookup"><span data-stu-id="bda95-209">You see the following error.</span></span>

`Error: Cloud service cannot connect to gateway through service bus.`

#### <a name="cause"></a><span data-ttu-id="bda95-210">Cause</span><span class="sxs-lookup"><span data-stu-id="bda95-210">Cause</span></span>
<span data-ttu-id="bda95-211">A transient error in network connectivity.</span><span class="sxs-lookup"><span data-stu-id="bda95-211">A transient error in network connectivity.</span></span>

#### <a name="resolution"></a><span data-ttu-id="bda95-212">Resolution</span><span class="sxs-lookup"><span data-stu-id="bda95-212">Resolution</span></span>
<span data-ttu-id="bda95-213">Follow these steps to get the gateway back online:</span><span class="sxs-lookup"><span data-stu-id="bda95-213">Follow these steps to get the gateway back online:</span></span>

1. <span data-ttu-id="bda95-214">Wait for a couple of minutes, the connectivity will be automatically recovered when the error is gone.</span><span class="sxs-lookup"><span data-stu-id="bda95-214">Wait for a couple of minutes, the connectivity will be automatically recovered when the error is gone.</span></span>
* <span data-ttu-id="bda95-215">If the error persists, restart the gateway service.</span><span class="sxs-lookup"><span data-stu-id="bda95-215">If the error persists, restart the gateway service.</span></span>

## <a name="failed-to-author-linked-service"></a><span data-ttu-id="bda95-216">Failed to author linked service</span><span class="sxs-lookup"><span data-stu-id="bda95-216">Failed to author linked service</span></span>
### <a name="problem"></a><span data-ttu-id="bda95-217">Problem</span><span class="sxs-lookup"><span data-stu-id="bda95-217">Problem</span></span>
<span data-ttu-id="bda95-218">You might see this error when you try to use Credential Manager in the portal to input credentials for a new linked service, or update credentials for an existing linked service.</span><span class="sxs-lookup"><span data-stu-id="bda95-218">You might see this error when you try to use Credential Manager in the portal to input credentials for a new linked service, or update credentials for an existing linked service.</span></span>

`Error: The data store '<Server>/<Database>' cannot be reached. Check connection settings for the data source.`

<span data-ttu-id="bda95-219">When you see this error, the settings page of Data Management Gateway Configuration Manager might look like the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="bda95-219">When you see this error, the settings page of Data Management Gateway Configuration Manager might look like the following screenshot.</span></span>

![Database cannot be reached](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a><span data-ttu-id="bda95-221">Cause</span><span class="sxs-lookup"><span data-stu-id="bda95-221">Cause</span></span>
<span data-ttu-id="bda95-222">The SSL certificate might have been lost on the gateway machine.</span><span class="sxs-lookup"><span data-stu-id="bda95-222">The SSL certificate might have been lost on the gateway machine.</span></span> <span data-ttu-id="bda95-223">The gateway computer cannot load the certificate currently that is used for SSL encryption.</span><span class="sxs-lookup"><span data-stu-id="bda95-223">The gateway computer cannot load the certificate currently that is used for SSL encryption.</span></span> <span data-ttu-id="bda95-224">You might also see an error message in the event log that is similar to the following message.</span><span class="sxs-lookup"><span data-stu-id="bda95-224">You might also see an error message in the event log that is similar to the following message.</span></span>

 `Unable to get the gateway settings from cloud service. Check the gateway key and the network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a><span data-ttu-id="bda95-225">Resolution</span><span class="sxs-lookup"><span data-stu-id="bda95-225">Resolution</span></span>
<span data-ttu-id="bda95-226">Follow these steps to solve the problem:</span><span class="sxs-lookup"><span data-stu-id="bda95-226">Follow these steps to solve the problem:</span></span>

1. <span data-ttu-id="bda95-227">Start Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="bda95-227">Start Data Management Gateway Configuration Manager.</span></span>
2. <span data-ttu-id="bda95-228">Switch to the **Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="bda95-228">Switch to the **Settings** tab.</span></span>  
3. <span data-ttu-id="bda95-229">Click the **Change** button to change the SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="bda95-229">Click the **Change** button to change the SSL certificate.</span></span>

   ![Change certificate button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. <span data-ttu-id="bda95-231">Select a new certificate as the SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="bda95-231">Select a new certificate as the SSL certificate.</span></span> <span data-ttu-id="bda95-232">You can use any SSL certificate that is generated by you or any organization.</span><span class="sxs-lookup"><span data-stu-id="bda95-232">You can use any SSL certificate that is generated by you or any organization.</span></span>

   ![Specify certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a><span data-ttu-id="bda95-234">Copy activity fails</span><span class="sxs-lookup"><span data-stu-id="bda95-234">Copy activity fails</span></span>
### <a name="problem"></a><span data-ttu-id="bda95-235">Problem</span><span class="sxs-lookup"><span data-stu-id="bda95-235">Problem</span></span>
<span data-ttu-id="bda95-236">You might notice the following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in the portal.</span><span class="sxs-lookup"><span data-stu-id="bda95-236">You might notice the following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in the portal.</span></span>

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect to SQL Server`

#### <a name="cause"></a><span data-ttu-id="bda95-237">Cause</span><span class="sxs-lookup"><span data-stu-id="bda95-237">Cause</span></span>
<span data-ttu-id="bda95-238">This can happen for different reasons, and mitigation varies accordingly.</span><span class="sxs-lookup"><span data-stu-id="bda95-238">This can happen for different reasons, and mitigation varies accordingly.</span></span>

#### <a name="resolution"></a><span data-ttu-id="bda95-239">Resolution</span><span class="sxs-lookup"><span data-stu-id="bda95-239">Resolution</span></span>
<span data-ttu-id="bda95-240">Allow outbound TCP connections over port TCP/1433 on the Data Management Gateway client side before connecting to an SQL database.</span><span class="sxs-lookup"><span data-stu-id="bda95-240">Allow outbound TCP connections over port TCP/1433 on the Data Management Gateway client side before connecting to an SQL database.</span></span>

<span data-ttu-id="bda95-241">If the target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span><span class="sxs-lookup"><span data-stu-id="bda95-241">If the target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span></span>

<span data-ttu-id="bda95-242">See the following section to test the connection to the on-premises data store.</span><span class="sxs-lookup"><span data-stu-id="bda95-242">See the following section to test the connection to the on-premises data store.</span></span>

## <a name="data-store-connection-or-driver-related-errors"></a><span data-ttu-id="bda95-243">Data store connection or driver-related errors</span><span class="sxs-lookup"><span data-stu-id="bda95-243">Data store connection or driver-related errors</span></span>
<span data-ttu-id="bda95-244">If you see data store connection or driver-related errors, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="bda95-244">If you see data store connection or driver-related errors, complete the following steps:</span></span>

1. <span data-ttu-id="bda95-245">Start Data Management Gateway Configuration Manager on the gateway machine.</span><span class="sxs-lookup"><span data-stu-id="bda95-245">Start Data Management Gateway Configuration Manager on the gateway machine.</span></span>
2. <span data-ttu-id="bda95-246">Switch to the **Diagnostics** tab.</span><span class="sxs-lookup"><span data-stu-id="bda95-246">Switch to the **Diagnostics** tab.</span></span>
3. <span data-ttu-id="bda95-247">In **Test Connection**, add the gateway group values.</span><span class="sxs-lookup"><span data-stu-id="bda95-247">In **Test Connection**, add the gateway group values.</span></span>
4. <span data-ttu-id="bda95-248">Click **Test** to see if you can connect to the on-premises data source from the gateway machine by using the connection information and credentials.</span><span class="sxs-lookup"><span data-stu-id="bda95-248">Click **Test** to see if you can connect to the on-premises data source from the gateway machine by using the connection information and credentials.</span></span> <span data-ttu-id="bda95-249">If the test connection still fails after you install a driver, restart the gateway for it to pick up the latest change.</span><span class="sxs-lookup"><span data-stu-id="bda95-249">If the test connection still fails after you install a driver, restart the gateway for it to pick up the latest change.</span></span>

![Test Connection in Diagnostics tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a><span data-ttu-id="bda95-251">Gateway logs</span><span class="sxs-lookup"><span data-stu-id="bda95-251">Gateway logs</span></span>
### <a name="send-gateway-logs-to-microsoft"></a><span data-ttu-id="bda95-252">Send gateway logs to Microsoft</span><span class="sxs-lookup"><span data-stu-id="bda95-252">Send gateway logs to Microsoft</span></span>
<span data-ttu-id="bda95-253">When you contact Microsoft Support to get help with troubleshooting gateway issues, you might be asked to share your gateway logs.</span><span class="sxs-lookup"><span data-stu-id="bda95-253">When you contact Microsoft Support to get help with troubleshooting gateway issues, you might be asked to share your gateway logs.</span></span> <span data-ttu-id="bda95-254">With the release of the gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="bda95-254">With the release of the gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span></span>    

1. <span data-ttu-id="bda95-255">Switch to the **Diagnostics** tab in Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="bda95-255">Switch to the **Diagnostics** tab in Data Management Gateway Configuration Manager.</span></span>

    ![Data Management Gateway Diagnostics tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. <span data-ttu-id="bda95-257">Click **Send Logs** to see the following dialog box.</span><span class="sxs-lookup"><span data-stu-id="bda95-257">Click **Send Logs** to see the following dialog box.</span></span>

    ![Data Management Gateway Send logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. <span data-ttu-id="bda95-259">(Optional) Click **view logs** to review logs in the event viewer.</span><span class="sxs-lookup"><span data-stu-id="bda95-259">(Optional) Click **view logs** to review logs in the event viewer.</span></span>
4. <span data-ttu-id="bda95-260">(Optional) Click **privacy** to review Microsoft web services privacy statement.</span><span class="sxs-lookup"><span data-stu-id="bda95-260">(Optional) Click **privacy** to review Microsoft web services privacy statement.</span></span>
5. <span data-ttu-id="bda95-261">When you are satisfied with what you are about to upload, click **Send Logs** to actually send the logs from the last seven days to Microsoft for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="bda95-261">When you are satisfied with what you are about to upload, click **Send Logs** to actually send the logs from the last seven days to Microsoft for troubleshooting.</span></span> <span data-ttu-id="bda95-262">You should see the status of the send-logs operation as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="bda95-262">You should see the status of the send-logs operation as shown in the following screenshot.</span></span>

    ![Data Management Gateway Send logs status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. <span data-ttu-id="bda95-264">After the operation is complete, you see a dialog box as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="bda95-264">After the operation is complete, you see a dialog box as shown in the following screenshot.</span></span>

    ![Data Management Gateway Send logs status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. <span data-ttu-id="bda95-266">Save the **Report ID** and share it with Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="bda95-266">Save the **Report ID** and share it with Microsoft Support.</span></span> <span data-ttu-id="bda95-267">The report ID is used to locate the gateway logs that you uploaded for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="bda95-267">The report ID is used to locate the gateway logs that you uploaded for troubleshooting.</span></span>  <span data-ttu-id="bda95-268">The report ID is also saved in the event viewer.</span><span class="sxs-lookup"><span data-stu-id="bda95-268">The report ID is also saved in the event viewer.</span></span>  <span data-ttu-id="bda95-269">You can find it by looking at the event ID “25”, and check the date and time.</span><span class="sxs-lookup"><span data-stu-id="bda95-269">You can find it by looking at the event ID “25”, and check the date and time.</span></span>

    ![Data Management Gateway Send logs report ID](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a><span data-ttu-id="bda95-271">Archive gateway logs on gateway host machine</span><span class="sxs-lookup"><span data-stu-id="bda95-271">Archive gateway logs on gateway host machine</span></span>
<span data-ttu-id="bda95-272">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span><span class="sxs-lookup"><span data-stu-id="bda95-272">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span></span>

* <span data-ttu-id="bda95-273">You manually install the gateway and register the gateway.</span><span class="sxs-lookup"><span data-stu-id="bda95-273">You manually install the gateway and register the gateway.</span></span>
* <span data-ttu-id="bda95-274">You try to register the gateway with a regenerated key in Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="bda95-274">You try to register the gateway with a regenerated key in Data Management Gateway Configuration Manager.</span></span>
* <span data-ttu-id="bda95-275">You try to send logs and the gateway host service cannot be connected.</span><span class="sxs-lookup"><span data-stu-id="bda95-275">You try to send logs and the gateway host service cannot be connected.</span></span>

<span data-ttu-id="bda95-276">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span><span class="sxs-lookup"><span data-stu-id="bda95-276">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span></span> <span data-ttu-id="bda95-277">For example, if you receive an error while you register the gateway as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="bda95-277">For example, if you receive an error while you register the gateway as shown in the following screenshot.</span></span>   

![Data Management Gateway Registration error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

<span data-ttu-id="bda95-279">Click the **Archive gateway logs** link to archive and save logs, and then share the zip file with Microsoft support.</span><span class="sxs-lookup"><span data-stu-id="bda95-279">Click the **Archive gateway logs** link to archive and save logs, and then share the zip file with Microsoft support.</span></span>

![Data Management Gateway Archive logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a><span data-ttu-id="bda95-281">Locate gateway logs</span><span class="sxs-lookup"><span data-stu-id="bda95-281">Locate gateway logs</span></span>
<span data-ttu-id="bda95-282">You can find detailed gateway log information in the Windows event logs.</span><span class="sxs-lookup"><span data-stu-id="bda95-282">You can find detailed gateway log information in the Windows event logs.</span></span>

1. <span data-ttu-id="bda95-283">Start Windows **Event Viewer**.</span><span class="sxs-lookup"><span data-stu-id="bda95-283">Start Windows **Event Viewer**.</span></span>
2. <span data-ttu-id="bda95-284">Locate logs in the **Application and Services Logs** > **Data Management Gateway** folder.</span><span class="sxs-lookup"><span data-stu-id="bda95-284">Locate logs in the **Application and Services Logs** > **Data Management Gateway** folder.</span></span>

 <span data-ttu-id="bda95-285">When you're troubleshooting gateway-related issues, look for error level events in the event viewer.</span><span class="sxs-lookup"><span data-stu-id="bda95-285">When you're troubleshooting gateway-related issues, look for error level events in the event viewer.</span></span>

![Data Management Gateway logs in event viewer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)


















