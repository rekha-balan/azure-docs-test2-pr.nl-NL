---
title: Troubleshoot domain and SSL certificate problems in Azure web apps | Microsoft Docs
description: Troubleshoot domain and SSL certificate problems in Azure web apps
services: app-service\web
documentationcenter: ''
author: genlin
manager: cshepard
editor: ''
tags: top-support-issue
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2018
ms.author: genli
ms.openlocfilehash: 5dd87c75638c3d084226becaace5c9454660c907
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866519"
---
# <a name="troubleshoot-domain-and-ssl-certificate-problems-in-azure-web-apps"></a><span data-ttu-id="f2e1f-103">Troubleshoot domain and SSL certificate problems in Azure web apps</span><span class="sxs-lookup"><span data-stu-id="f2e1f-103">Troubleshoot domain and SSL certificate problems in Azure web apps</span></span>

<span data-ttu-id="f2e1f-104">This article lists common problems that you might encounter when you configure a domain or SSL certificate for your Azure web apps.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-104">This article lists common problems that you might encounter when you configure a domain or SSL certificate for your Azure web apps.</span></span> <span data-ttu-id="f2e1f-105">It also describes possible causes and solutions for these problems.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-105">It also describes possible causes and solutions for these problems.</span></span>

<span data-ttu-id="f2e1f-106">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="f2e1f-106">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="f2e1f-107">Alternatively, you can file an Azure support incident.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-107">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="f2e1f-108">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-108">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="certificate-problems"></a><span data-ttu-id="f2e1f-109">Certificate problems</span><span class="sxs-lookup"><span data-stu-id="f2e1f-109">Certificate problems</span></span>

### <a name="you-cant-add-an-ssl-certificate-binding-to-a-web-app"></a><span data-ttu-id="f2e1f-110">You can't add an SSL certificate binding to a web app</span><span class="sxs-lookup"><span data-stu-id="f2e1f-110">You can't add an SSL certificate binding to a web app</span></span> 

#### <a name="symptom"></a><span data-ttu-id="f2e1f-111">Symptom</span><span class="sxs-lookup"><span data-stu-id="f2e1f-111">Symptom</span></span>

<span data-ttu-id="f2e1f-112">When you add an SSL binding, you receive the following error message:</span><span class="sxs-lookup"><span data-stu-id="f2e1f-112">When you add an SSL binding, you receive the following error message:</span></span>

<span data-ttu-id="f2e1f-113">"Failed to add SSL binding.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-113">"Failed to add SSL binding.</span></span> <span data-ttu-id="f2e1f-114">Cannot set certificate for existing VIP because another VIP already uses that certificate."</span><span class="sxs-lookup"><span data-stu-id="f2e1f-114">Cannot set certificate for existing VIP because another VIP already uses that certificate."</span></span>

#### <a name="cause"></a><span data-ttu-id="f2e1f-115">Cause</span><span class="sxs-lookup"><span data-stu-id="f2e1f-115">Cause</span></span>

<span data-ttu-id="f2e1f-116">This problem can occur if you have multiple IP-based SSL bindings for the same IP address across multiple web apps.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-116">This problem can occur if you have multiple IP-based SSL bindings for the same IP address across multiple web apps.</span></span> <span data-ttu-id="f2e1f-117">For example, web app A has an IP-based SSL with an old certificate.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-117">For example, web app A has an IP-based SSL with an old certificate.</span></span> <span data-ttu-id="f2e1f-118">Web app B has an IP-based SSL with a new certificate for the same IP address.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-118">Web app B has an IP-based SSL with a new certificate for the same IP address.</span></span> <span data-ttu-id="f2e1f-119">When you update the web app SSL binding with the new certificate, it fails with this error because the same IP address is being used for another app.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-119">When you update the web app SSL binding with the new certificate, it fails with this error because the same IP address is being used for another app.</span></span> 

#### <a name="solution"></a><span data-ttu-id="f2e1f-120">Solution</span><span class="sxs-lookup"><span data-stu-id="f2e1f-120">Solution</span></span> 

<span data-ttu-id="f2e1f-121">To fix this problem, use one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="f2e1f-121">To fix this problem, use one of the following methods:</span></span>

- <span data-ttu-id="f2e1f-122">Delete the IP-based SSL binding on the web app that uses the old certificate.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-122">Delete the IP-based SSL binding on the web app that uses the old certificate.</span></span> 
- <span data-ttu-id="f2e1f-123">Create a new IP-based SSL binding that uses the new certificate.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-123">Create a new IP-based SSL binding that uses the new certificate.</span></span>

### <a name="you-cant-delete-a-certificate"></a><span data-ttu-id="f2e1f-124">You can't delete a certificate</span><span class="sxs-lookup"><span data-stu-id="f2e1f-124">You can't delete a certificate</span></span> 

#### <a name="symptom"></a><span data-ttu-id="f2e1f-125">Symptom</span><span class="sxs-lookup"><span data-stu-id="f2e1f-125">Symptom</span></span>

<span data-ttu-id="f2e1f-126">When you try to delete a certificate, you receive the following error message:</span><span class="sxs-lookup"><span data-stu-id="f2e1f-126">When you try to delete a certificate, you receive the following error message:</span></span>

<span data-ttu-id="f2e1f-127">"Unable to delete the certificate because it is currently being used in an SSL binding.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-127">"Unable to delete the certificate because it is currently being used in an SSL binding.</span></span> <span data-ttu-id="f2e1f-128">The SSL binding must be removed before you can delete the certificate."</span><span class="sxs-lookup"><span data-stu-id="f2e1f-128">The SSL binding must be removed before you can delete the certificate."</span></span>

#### <a name="cause"></a><span data-ttu-id="f2e1f-129">Cause</span><span class="sxs-lookup"><span data-stu-id="f2e1f-129">Cause</span></span>

<span data-ttu-id="f2e1f-130">This problem might occur if another web app uses the certificate.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-130">This problem might occur if another web app uses the certificate.</span></span>

#### <a name="solution"></a><span data-ttu-id="f2e1f-131">Solution</span><span class="sxs-lookup"><span data-stu-id="f2e1f-131">Solution</span></span>

<span data-ttu-id="f2e1f-132">Remove the SSL binding for that certificate from the web apps.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-132">Remove the SSL binding for that certificate from the web apps.</span></span> <span data-ttu-id="f2e1f-133">Then try to delete the certificate.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-133">Then try to delete the certificate.</span></span> <span data-ttu-id="f2e1f-134">If you still can't delete the certificate, clear the internet browser cache and reopen the Azure portal in a new browser window.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-134">If you still can't delete the certificate, clear the internet browser cache and reopen the Azure portal in a new browser window.</span></span> <span data-ttu-id="f2e1f-135">Then try to delete the certificate.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-135">Then try to delete the certificate.</span></span>

### <a name="you-cant-purchase-an-app-service-certificate"></a><span data-ttu-id="f2e1f-136">You can't purchase an App Service certificate</span><span class="sxs-lookup"><span data-stu-id="f2e1f-136">You can't purchase an App Service certificate</span></span> 

#### <a name="symptom"></a><span data-ttu-id="f2e1f-137">Symptom</span><span class="sxs-lookup"><span data-stu-id="f2e1f-137">Symptom</span></span>
<span data-ttu-id="f2e1f-138">You can't purchase an [Azure App Service certificate](./web-sites-purchase-ssl-web-site.md) from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-138">You can't purchase an [Azure App Service certificate](./web-sites-purchase-ssl-web-site.md) from the Azure portal.</span></span>

#### <a name="cause-and-solution"></a><span data-ttu-id="f2e1f-139">Cause and solution</span><span class="sxs-lookup"><span data-stu-id="f2e1f-139">Cause and solution</span></span>
<span data-ttu-id="f2e1f-140">This problem can occur for any of the following reasons:</span><span class="sxs-lookup"><span data-stu-id="f2e1f-140">This problem can occur for any of the following reasons:</span></span>

- <span data-ttu-id="f2e1f-141">The App Service plan is Free or Shared.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-141">The App Service plan is Free or Shared.</span></span> <span data-ttu-id="f2e1f-142">These pricing tiers don't support SSL.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-142">These pricing tiers don't support SSL.</span></span> 

    <span data-ttu-id="f2e1f-143">**Solution**: Upgrade the App Service plan for web app to Standard.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-143">**Solution**: Upgrade the App Service plan for web app to Standard.</span></span>

- <span data-ttu-id="f2e1f-144">The subscription doesn't have a valid credit card.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-144">The subscription doesn't have a valid credit card.</span></span>

    <span data-ttu-id="f2e1f-145">**Solution**: Add a valid credit card to your subscription.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-145">**Solution**: Add a valid credit card to your subscription.</span></span> 

- <span data-ttu-id="f2e1f-146">The subscription offer doesn't support purchasing an App Service certificate such as Microsoft Student.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-146">The subscription offer doesn't support purchasing an App Service certificate such as Microsoft Student.</span></span>  

    <span data-ttu-id="f2e1f-147">**Solution**: Upgrade your subscription.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-147">**Solution**: Upgrade your subscription.</span></span> 

- <span data-ttu-id="f2e1f-148">The subscription reached the limit of purchases that are allowed on a subscription.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-148">The subscription reached the limit of purchases that are allowed on a subscription.</span></span>

    <span data-ttu-id="f2e1f-149">**Solution**: App Service certificates have a limit of 10 certificate purchases for the Pay-As-You-Go and EA subscription types.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-149">**Solution**: App Service certificates have a limit of 10 certificate purchases for the Pay-As-You-Go and EA subscription types.</span></span> <span data-ttu-id="f2e1f-150">For other subscription types, the limit is 3.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-150">For other subscription types, the limit is 3.</span></span> <span data-ttu-id="f2e1f-151">To increase the limit, contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="f2e1f-151">To increase the limit, contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
- <span data-ttu-id="f2e1f-152">The App Service certificate was marked as fraud.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-152">The App Service certificate was marked as fraud.</span></span> <span data-ttu-id="f2e1f-153">You received the following error message: "Your certificate has been flagged for possible fraud.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-153">You received the following error message: "Your certificate has been flagged for possible fraud.</span></span> <span data-ttu-id="f2e1f-154">The request is currently under review.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-154">The request is currently under review.</span></span> <span data-ttu-id="f2e1f-155">If the certificate does not become usable within 24 hours, please contact Azure Support."</span><span class="sxs-lookup"><span data-stu-id="f2e1f-155">If the certificate does not become usable within 24 hours, please contact Azure Support."</span></span>

    <span data-ttu-id="f2e1f-156">**Solution**: If the certificate is marked as fraud and isn't resolved after 24 hours, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f2e1f-156">**Solution**: If the certificate is marked as fraud and isn't resolved after 24 hours, follow these steps:</span></span>

    1. <span data-ttu-id="f2e1f-157">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f2e1f-157">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
    2. <span data-ttu-id="f2e1f-158">Go to **App Service Certificates**, and select the certificate.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-158">Go to **App Service Certificates**, and select the certificate.</span></span>
    3. <span data-ttu-id="f2e1f-159">Select **Certificate Configuration** > **Step 2: Verify** > **Domain Verification**.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-159">Select **Certificate Configuration** > **Step 2: Verify** > **Domain Verification**.</span></span> <span data-ttu-id="f2e1f-160">This step sends an email notice to the Azure certificate provider to resolve the problem.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-160">This step sends an email notice to the Azure certificate provider to resolve the problem.</span></span>

## <a name="domain-problems"></a><span data-ttu-id="f2e1f-161">Domain problems</span><span class="sxs-lookup"><span data-stu-id="f2e1f-161">Domain problems</span></span>

### <a name="you-purchased-an-ssl-certificate-for-the-wrong-domain"></a><span data-ttu-id="f2e1f-162">You purchased an SSL certificate for the wrong domain</span><span class="sxs-lookup"><span data-stu-id="f2e1f-162">You purchased an SSL certificate for the wrong domain</span></span>

#### <a name="symptom"></a><span data-ttu-id="f2e1f-163">Symptom</span><span class="sxs-lookup"><span data-stu-id="f2e1f-163">Symptom</span></span>

<span data-ttu-id="f2e1f-164">You purchased an App Service certificate for the wrong domain.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-164">You purchased an App Service certificate for the wrong domain.</span></span> <span data-ttu-id="f2e1f-165">You can't update the certificate to use the correct domain.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-165">You can't update the certificate to use the correct domain.</span></span>

#### <a name="solution"></a><span data-ttu-id="f2e1f-166">Solution</span><span class="sxs-lookup"><span data-stu-id="f2e1f-166">Solution</span></span>

<span data-ttu-id="f2e1f-167">Delete that certificate and then buy a new certificate.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-167">Delete that certificate and then buy a new certificate.</span></span>

<span data-ttu-id="f2e1f-168">If the current certificate that uses the wrong domain is in the “Issued” state, you'll also be billed for that certificate.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-168">If the current certificate that uses the wrong domain is in the “Issued” state, you'll also be billed for that certificate.</span></span> <span data-ttu-id="f2e1f-169">App Service certificates are not refundable, but you can contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to see whether there are other options.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-169">App Service certificates are not refundable, but you can contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to see whether there are other options.</span></span> 

### <a name="an-app-service-certificate-was-renewed-but-the-web-app-shows-the-old-certificate"></a><span data-ttu-id="f2e1f-170">An App Service certificate was renewed, but the web app shows the old certificate</span><span class="sxs-lookup"><span data-stu-id="f2e1f-170">An App Service certificate was renewed, but the web app shows the old certificate</span></span> 

#### <a name="symptom"></a><span data-ttu-id="f2e1f-171">Symptom</span><span class="sxs-lookup"><span data-stu-id="f2e1f-171">Symptom</span></span>

<span data-ttu-id="f2e1f-172">The App Service certificate was renewed, but the web app that uses the App Service certificate is still using the old certificate.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-172">The App Service certificate was renewed, but the web app that uses the App Service certificate is still using the old certificate.</span></span> <span data-ttu-id="f2e1f-173">Also, you received a warning that the HTTPS protocol is required.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-173">Also, you received a warning that the HTTPS protocol is required.</span></span>

#### <a name="cause"></a><span data-ttu-id="f2e1f-174">Cause</span><span class="sxs-lookup"><span data-stu-id="f2e1f-174">Cause</span></span> 
<span data-ttu-id="f2e1f-175">The Web Apps feature of Azure App Service runs a background job every eight hours and syncs the certificate resource if there are any changes.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-175">The Web Apps feature of Azure App Service runs a background job every eight hours and syncs the certificate resource if there are any changes.</span></span> <span data-ttu-id="f2e1f-176">When you rotate or update a certificate, sometimes the application is still retrieving the old certificate and not the newly updated certificate.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-176">When you rotate or update a certificate, sometimes the application is still retrieving the old certificate and not the newly updated certificate.</span></span> <span data-ttu-id="f2e1f-177">The reason is that the job to sync the certificate resource hasn't run yet.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-177">The reason is that the job to sync the certificate resource hasn't run yet.</span></span> 
 
#### <a name="solution"></a><span data-ttu-id="f2e1f-178">Solution</span><span class="sxs-lookup"><span data-stu-id="f2e1f-178">Solution</span></span>

<span data-ttu-id="f2e1f-179">You can force a sync of the certificate:</span><span class="sxs-lookup"><span data-stu-id="f2e1f-179">You can force a sync of the certificate:</span></span>

1. <span data-ttu-id="f2e1f-180">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f2e1f-180">Sign in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f2e1f-181">Select **App Service Certificates**, and then select the certificate.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-181">Select **App Service Certificates**, and then select the certificate.</span></span>
2. <span data-ttu-id="f2e1f-182">Select **Rekey and Sync**, and then select **Sync**. The sync takes some time to finish.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-182">Select **Rekey and Sync**, and then select **Sync**. The sync takes some time to finish.</span></span> 
3. <span data-ttu-id="f2e1f-183">When the sync is completed, you see the following notification: "Successfully updated all the resources with the latest certificate."</span><span class="sxs-lookup"><span data-stu-id="f2e1f-183">When the sync is completed, you see the following notification: "Successfully updated all the resources with the latest certificate."</span></span>

### <a name="domain-verification-is-not-working"></a><span data-ttu-id="f2e1f-184">Domain verification is not working</span><span class="sxs-lookup"><span data-stu-id="f2e1f-184">Domain verification is not working</span></span> 

#### <a name="symptom"></a><span data-ttu-id="f2e1f-185">Symptom</span><span class="sxs-lookup"><span data-stu-id="f2e1f-185">Symptom</span></span> 
<span data-ttu-id="f2e1f-186">The App Service certificate requires domain verification before the certificate is ready to use.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-186">The App Service certificate requires domain verification before the certificate is ready to use.</span></span> <span data-ttu-id="f2e1f-187">When you select **Verify**, the process fails.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-187">When you select **Verify**, the process fails.</span></span>

#### <a name="solution"></a><span data-ttu-id="f2e1f-188">Solution</span><span class="sxs-lookup"><span data-stu-id="f2e1f-188">Solution</span></span>
<span data-ttu-id="f2e1f-189">Manually verify your domain by adding a TXT record:</span><span class="sxs-lookup"><span data-stu-id="f2e1f-189">Manually verify your domain by adding a TXT record:</span></span>
 
1.  <span data-ttu-id="f2e1f-190">Go to the Domain Name Service (DNS) provider that hosts your domain name.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-190">Go to the Domain Name Service (DNS) provider that hosts your domain name.</span></span>
2.  <span data-ttu-id="f2e1f-191">Add a TXT record for your domain that uses the value of the domain token that's shown in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-191">Add a TXT record for your domain that uses the value of the domain token that's shown in the Azure portal.</span></span> 

<span data-ttu-id="f2e1f-192">Wait a few minutes for DNS propagation to run, and then select the **Refresh** button to trigger the verification.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-192">Wait a few minutes for DNS propagation to run, and then select the **Refresh** button to trigger the verification.</span></span> 

<span data-ttu-id="f2e1f-193">As an alternative, you can use the HTML webpage method to manually verify your domain.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-193">As an alternative, you can use the HTML webpage method to manually verify your domain.</span></span> <span data-ttu-id="f2e1f-194">This method allows the certificate authority to confirm the domain ownership of the domain that the certificate is issued for.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-194">This method allows the certificate authority to confirm the domain ownership of the domain that the certificate is issued for.</span></span>

1.  <span data-ttu-id="f2e1f-195">Create an HTML file that's named {domain verification token}.html.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-195">Create an HTML file that's named {domain verification token}.html.</span></span> <span data-ttu-id="f2e1f-196">The content of this file should be the value of domain verification token.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-196">The content of this file should be the value of domain verification token.</span></span>
3.  <span data-ttu-id="f2e1f-197">Upload this file at the root of the web server that's hosting your domain.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-197">Upload this file at the root of the web server that's hosting your domain.</span></span>
4.  <span data-ttu-id="f2e1f-198">Select **Refresh** to check the certificate status.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-198">Select **Refresh** to check the certificate status.</span></span> <span data-ttu-id="f2e1f-199">It might take few minutes for verification to finish.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-199">It might take few minutes for verification to finish.</span></span>

<span data-ttu-id="f2e1f-200">For example, if you're buying a standard certificate for azure.com with the domain verification token 1234abcd, a web request made to http://azure.com/1234abcd.html should return 1234abcd.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-200">For example, if you're buying a standard certificate for azure.com with the domain verification token 1234abcd, a web request made to http://azure.com/1234abcd.html should return 1234abcd.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f2e1f-201">A certificate order has only 15 days to complete the domain verification operation.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-201">A certificate order has only 15 days to complete the domain verification operation.</span></span> <span data-ttu-id="f2e1f-202">After 15 days, the certificate authority denies the certificate, and you are not charged for the certificate.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-202">After 15 days, the certificate authority denies the certificate, and you are not charged for the certificate.</span></span> <span data-ttu-id="f2e1f-203">In this situation, delete this certificate and try again.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-203">In this situation, delete this certificate and try again.</span></span>
>
> 

### <a name="you-cant-purchase-a-domain"></a><span data-ttu-id="f2e1f-204">You can't purchase a domain</span><span class="sxs-lookup"><span data-stu-id="f2e1f-204">You can't purchase a domain</span></span>

#### <a name="symptom"></a><span data-ttu-id="f2e1f-205">Symptom</span><span class="sxs-lookup"><span data-stu-id="f2e1f-205">Symptom</span></span>
<span data-ttu-id="f2e1f-206">You can't buy a domain from the Web Apps or App Service domain in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-206">You can't buy a domain from the Web Apps or App Service domain in the Azure portal.</span></span>

#### <a name="cause-and-solution"></a><span data-ttu-id="f2e1f-207">Cause and solution</span><span class="sxs-lookup"><span data-stu-id="f2e1f-207">Cause and solution</span></span>

<span data-ttu-id="f2e1f-208">This problem occurs for one of the following reasons:</span><span class="sxs-lookup"><span data-stu-id="f2e1f-208">This problem occurs for one of the following reasons:</span></span>

- <span data-ttu-id="f2e1f-209">There's no credit card on the Azure subscription, or the credit card is invalid.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-209">There's no credit card on the Azure subscription, or the credit card is invalid.</span></span>

    <span data-ttu-id="f2e1f-210">**Solution**: Add a valid credit card to your subscription.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-210">**Solution**: Add a valid credit card to your subscription.</span></span>

- <span data-ttu-id="f2e1f-211">You're not the subscription owner, so you don't have permission to purchase a domain.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-211">You're not the subscription owner, so you don't have permission to purchase a domain.</span></span>

    <span data-ttu-id="f2e1f-212">**Solution**: [Assign the Owner role](../role-based-access-control/role-assignments-portal.md) to your account.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-212">**Solution**: [Assign the Owner role](../role-based-access-control/role-assignments-portal.md) to your account.</span></span> <span data-ttu-id="f2e1f-213">Or contact the subscription administrator to get permission to purchase a domain.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-213">Or contact the subscription administrator to get permission to purchase a domain.</span></span>
- <span data-ttu-id="f2e1f-214">You have reached the limit for purchasing domains on your subscription.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-214">You have reached the limit for purchasing domains on your subscription.</span></span> <span data-ttu-id="f2e1f-215">The current limit is 20.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-215">The current limit is 20.</span></span>

    <span data-ttu-id="f2e1f-216">**Solution**: To request an increase to the limit, contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="f2e1f-216">**Solution**: To request an increase to the limit, contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
- <span data-ttu-id="f2e1f-217">Your Azure subscription type does not support the purchase of an App Service domain.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-217">Your Azure subscription type does not support the purchase of an App Service domain.</span></span>

    <span data-ttu-id="f2e1f-218">**Solution**: Upgrade your Azure subscription to another subscription type, such as a Pay-As-You-Go subscription.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-218">**Solution**: Upgrade your Azure subscription to another subscription type, such as a Pay-As-You-Go subscription.</span></span>

### <a name="you-cant-add-a-host-name-to-a-web-app"></a><span data-ttu-id="f2e1f-219">You can't add a host name to a web app</span><span class="sxs-lookup"><span data-stu-id="f2e1f-219">You can't add a host name to a web app</span></span> 

#### <a name="symptom"></a><span data-ttu-id="f2e1f-220">Symptom</span><span class="sxs-lookup"><span data-stu-id="f2e1f-220">Symptom</span></span>

<span data-ttu-id="f2e1f-221">When you add a host name, the process fails to validate and verify the domain.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-221">When you add a host name, the process fails to validate and verify the domain.</span></span>

#### <a name="cause"></a><span data-ttu-id="f2e1f-222">Cause</span><span class="sxs-lookup"><span data-stu-id="f2e1f-222">Cause</span></span> 

<span data-ttu-id="f2e1f-223">This problem occurs for one of the following reasons:</span><span class="sxs-lookup"><span data-stu-id="f2e1f-223">This problem occurs for one of the following reasons:</span></span>

- <span data-ttu-id="f2e1f-224">You don’t have permission to add a host name.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-224">You don’t have permission to add a host name.</span></span>

    <span data-ttu-id="f2e1f-225">**Solution**: Ask the subscription administrator to give you permission to add a host name.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-225">**Solution**: Ask the subscription administrator to give you permission to add a host name.</span></span>
- <span data-ttu-id="f2e1f-226">Your domain ownership could not be verified.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-226">Your domain ownership could not be verified.</span></span>

    <span data-ttu-id="f2e1f-227">**Solution**: Verify that your CNAME or A record is configured correctly.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-227">**Solution**: Verify that your CNAME or A record is configured correctly.</span></span> <span data-ttu-id="f2e1f-228">To map a custom domain to web app, create either a CNAME record or an A record.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-228">To map a custom domain to web app, create either a CNAME record or an A record.</span></span> <span data-ttu-id="f2e1f-229">If you want to use a root domain, you must use A and TXT records:</span><span class="sxs-lookup"><span data-stu-id="f2e1f-229">If you want to use a root domain, you must use A and TXT records:</span></span>

    |<span data-ttu-id="f2e1f-230">Record type</span><span class="sxs-lookup"><span data-stu-id="f2e1f-230">Record type</span></span>|<span data-ttu-id="f2e1f-231">Host</span><span class="sxs-lookup"><span data-stu-id="f2e1f-231">Host</span></span>|<span data-ttu-id="f2e1f-232">Point to</span><span class="sxs-lookup"><span data-stu-id="f2e1f-232">Point to</span></span>|
    |------|------|-----|
    |<span data-ttu-id="f2e1f-233">A</span><span class="sxs-lookup"><span data-stu-id="f2e1f-233">A</span></span>|@|<span data-ttu-id="f2e1f-234">IP address for a web app</span><span class="sxs-lookup"><span data-stu-id="f2e1f-234">IP address for a web app</span></span>|
    |<span data-ttu-id="f2e1f-235">TXT</span><span class="sxs-lookup"><span data-stu-id="f2e1f-235">TXT</span></span>|@|<span data-ttu-id="f2e1f-236"><app-name>.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="f2e1f-236"><app-name>.azurewebsites.net</span></span>|
    |<span data-ttu-id="f2e1f-237">CNAME</span><span class="sxs-lookup"><span data-stu-id="f2e1f-237">CNAME</span></span>|<span data-ttu-id="f2e1f-238">www</span><span class="sxs-lookup"><span data-stu-id="f2e1f-238">www</span></span>|<span data-ttu-id="f2e1f-239"><app-name>.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="f2e1f-239"><app-name>.azurewebsites.net</span></span>|

### <a name="dns-cant-be-resolved"></a><span data-ttu-id="f2e1f-240">DNS can't be resolved</span><span class="sxs-lookup"><span data-stu-id="f2e1f-240">DNS can't be resolved</span></span>

#### <a name="symptom"></a><span data-ttu-id="f2e1f-241">Symptom</span><span class="sxs-lookup"><span data-stu-id="f2e1f-241">Symptom</span></span>

<span data-ttu-id="f2e1f-242">You received the following error message:</span><span class="sxs-lookup"><span data-stu-id="f2e1f-242">You received the following error message:</span></span>

<span data-ttu-id="f2e1f-243">"The DNS record could not be located."</span><span class="sxs-lookup"><span data-stu-id="f2e1f-243">"The DNS record could not be located."</span></span>

#### <a name="cause"></a><span data-ttu-id="f2e1f-244">Cause</span><span class="sxs-lookup"><span data-stu-id="f2e1f-244">Cause</span></span>
<span data-ttu-id="f2e1f-245">This problem occurs for one of the following reasons:</span><span class="sxs-lookup"><span data-stu-id="f2e1f-245">This problem occurs for one of the following reasons:</span></span>

- <span data-ttu-id="f2e1f-246">The time to live (TTL) period has not expired.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-246">The time to live (TTL) period has not expired.</span></span> <span data-ttu-id="f2e1f-247">Check the DNS configuration for your domain to determine the TTL value, and then wait for the period to expire.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-247">Check the DNS configuration for your domain to determine the TTL value, and then wait for the period to expire.</span></span>
- <span data-ttu-id="f2e1f-248">The DNS configuration is incorrect.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-248">The DNS configuration is incorrect.</span></span>

#### <a name="solution"></a><span data-ttu-id="f2e1f-249">Solution</span><span class="sxs-lookup"><span data-stu-id="f2e1f-249">Solution</span></span>
- <span data-ttu-id="f2e1f-250">Wait for 48 hours for this problem to resolve itself.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-250">Wait for 48 hours for this problem to resolve itself.</span></span>
- <span data-ttu-id="f2e1f-251">If you can change the TTL setting in your DNS configuration, change the value to 5 minutes to see whether this resolves the problem.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-251">If you can change the TTL setting in your DNS configuration, change the value to 5 minutes to see whether this resolves the problem.</span></span>
- <span data-ttu-id="f2e1f-252">Use [WhatsmyDNS.net](https://www.whatsmydns.net/) to verify that your domain points to the web app's IP address.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-252">Use [WhatsmyDNS.net](https://www.whatsmydns.net/) to verify that your domain points to the web app's IP address.</span></span> <span data-ttu-id="f2e1f-253">If it doesn't, configure the A record to the correct IP address of the web app.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-253">If it doesn't, configure the A record to the correct IP address of the web app.</span></span>

### <a name="you-need-to-restore-a-deleted-domain"></a><span data-ttu-id="f2e1f-254">You need to restore a deleted domain</span><span class="sxs-lookup"><span data-stu-id="f2e1f-254">You need to restore a deleted domain</span></span> 

#### <a name="symptom"></a><span data-ttu-id="f2e1f-255">Symptom</span><span class="sxs-lookup"><span data-stu-id="f2e1f-255">Symptom</span></span>
<span data-ttu-id="f2e1f-256">Your domain is no longer visible in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-256">Your domain is no longer visible in the Azure portal.</span></span>

#### <a name="cause"></a><span data-ttu-id="f2e1f-257">Cause</span><span class="sxs-lookup"><span data-stu-id="f2e1f-257">Cause</span></span> 
<span data-ttu-id="f2e1f-258">The owner of the subscription might have accidentally deleted the domain.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-258">The owner of the subscription might have accidentally deleted the domain.</span></span>

#### <a name="solution"></a><span data-ttu-id="f2e1f-259">Solution</span><span class="sxs-lookup"><span data-stu-id="f2e1f-259">Solution</span></span>
<span data-ttu-id="f2e1f-260">If your domain was deleted fewer than seven days ago, the domain has not yet started the deletion process.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-260">If your domain was deleted fewer than seven days ago, the domain has not yet started the deletion process.</span></span> <span data-ttu-id="f2e1f-261">In this case, you can buy the same domain again on the Azure portal under the same subscription.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-261">In this case, you can buy the same domain again on the Azure portal under the same subscription.</span></span> <span data-ttu-id="f2e1f-262">(Be sure to type the exact domain name in the search box.) You won't be charged again for this domain.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-262">(Be sure to type the exact domain name in the search box.) You won't be charged again for this domain.</span></span> <span data-ttu-id="f2e1f-263">If the domain was deleted more than seven days ago, contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) for help to restore the domain.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-263">If the domain was deleted more than seven days ago, contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) for help to restore the domain.</span></span>

### <a name="a-custom-domain-returns-a-404-error"></a><span data-ttu-id="f2e1f-264">A custom domain returns a 404 error</span><span class="sxs-lookup"><span data-stu-id="f2e1f-264">A custom domain returns a 404 error</span></span> 

#### <a name="symptom"></a><span data-ttu-id="f2e1f-265">Symptom</span><span class="sxs-lookup"><span data-stu-id="f2e1f-265">Symptom</span></span>

<span data-ttu-id="f2e1f-266">When you browse to the site by using the custom domain name, you receive the following error message:</span><span class="sxs-lookup"><span data-stu-id="f2e1f-266">When you browse to the site by using the custom domain name, you receive the following error message:</span></span>

<span data-ttu-id="f2e1f-267">"Error 404-Web app not found."</span><span class="sxs-lookup"><span data-stu-id="f2e1f-267">"Error 404-Web app not found."</span></span>


#### <a name="cause-and-solution"></a><span data-ttu-id="f2e1f-268">Cause and solution</span><span class="sxs-lookup"><span data-stu-id="f2e1f-268">Cause and solution</span></span>

<span data-ttu-id="f2e1f-269">**Cause 1**</span><span class="sxs-lookup"><span data-stu-id="f2e1f-269">**Cause 1**</span></span> 

<span data-ttu-id="f2e1f-270">The custom domain that you configured is missing a CNAME or A record.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-270">The custom domain that you configured is missing a CNAME or A record.</span></span> 

<span data-ttu-id="f2e1f-271">**Solution for cause 1**</span><span class="sxs-lookup"><span data-stu-id="f2e1f-271">**Solution for cause 1**</span></span>

- <span data-ttu-id="f2e1f-272">If you added an A record, make sure that a TXT record is also added.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-272">If you added an A record, make sure that a TXT record is also added.</span></span> <span data-ttu-id="f2e1f-273">For more information, see [Create the A record](./app-service-web-tutorial-custom-domain.md#create-the-a-record).</span><span class="sxs-lookup"><span data-stu-id="f2e1f-273">For more information, see [Create the A record](./app-service-web-tutorial-custom-domain.md#create-the-a-record).</span></span>
- <span data-ttu-id="f2e1f-274">If you don't have to use the root domain for your web app, we recommend that you use a CNAME record instead of an A record.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-274">If you don't have to use the root domain for your web app, we recommend that you use a CNAME record instead of an A record.</span></span>
- <span data-ttu-id="f2e1f-275">Don't use both a CNAME record and an A record for the same domain.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-275">Don't use both a CNAME record and an A record for the same domain.</span></span> <span data-ttu-id="f2e1f-276">This can cause a conflict and prevent the domain from being resolved.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-276">This can cause a conflict and prevent the domain from being resolved.</span></span> 

<span data-ttu-id="f2e1f-277">**Cause 2**</span><span class="sxs-lookup"><span data-stu-id="f2e1f-277">**Cause 2**</span></span> 

<span data-ttu-id="f2e1f-278">The internet browser might still be caching the old IP address for your domain.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-278">The internet browser might still be caching the old IP address for your domain.</span></span> 

<span data-ttu-id="f2e1f-279">**Solution for Cause 2**</span><span class="sxs-lookup"><span data-stu-id="f2e1f-279">**Solution for Cause 2**</span></span>

<span data-ttu-id="f2e1f-280">Clear the browser.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-280">Clear the browser.</span></span> <span data-ttu-id="f2e1f-281">For Windows devices, you can run the command `ipconfig /flushdns`.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-281">For Windows devices, you can run the command `ipconfig /flushdns`.</span></span> <span data-ttu-id="f2e1f-282">Use [WhatsmyDNS.net](https://www.whatsmydns.net/) to verify that your domain points to the web app's IP address.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-282">Use [WhatsmyDNS.net](https://www.whatsmydns.net/) to verify that your domain points to the web app's IP address.</span></span> 

### <a name="you-cant-add-a-subdomain"></a><span data-ttu-id="f2e1f-283">You can't add a subdomain</span><span class="sxs-lookup"><span data-stu-id="f2e1f-283">You can't add a subdomain</span></span> 

#### <a name="symptom"></a><span data-ttu-id="f2e1f-284">Symptom</span><span class="sxs-lookup"><span data-stu-id="f2e1f-284">Symptom</span></span>

<span data-ttu-id="f2e1f-285">You can't add a new host name to a web app to assign a subdomain.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-285">You can't add a new host name to a web app to assign a subdomain.</span></span>

#### <a name="solution"></a><span data-ttu-id="f2e1f-286">Solution</span><span class="sxs-lookup"><span data-stu-id="f2e1f-286">Solution</span></span>

- <span data-ttu-id="f2e1f-287">Check with subscription administrator to make sure that you have permissions to add a host name to the web app.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-287">Check with subscription administrator to make sure that you have permissions to add a host name to the web app.</span></span>
- <span data-ttu-id="f2e1f-288">If you need more subdomains, we recommend that you change the domain hosting to Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-288">If you need more subdomains, we recommend that you change the domain hosting to Azure DNS.</span></span> <span data-ttu-id="f2e1f-289">By using Azure DNS, you can add 500 host names to your web app.</span><span class="sxs-lookup"><span data-stu-id="f2e1f-289">By using Azure DNS, you can add 500 host names to your web app.</span></span> <span data-ttu-id="f2e1f-290">For more information, see [Add a subdomain](https://blogs.msdn.microsoft.com/waws/2014/10/01/mapping-a-custom-subdomain-to-an-azure-website/).</span><span class="sxs-lookup"><span data-stu-id="f2e1f-290">For more information, see [Add a subdomain](https://blogs.msdn.microsoft.com/waws/2014/10/01/mapping-a-custom-subdomain-to-an-azure-website/).</span></span>











 


















