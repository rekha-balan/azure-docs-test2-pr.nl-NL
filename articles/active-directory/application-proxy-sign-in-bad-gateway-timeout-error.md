---
<span data-ttu-id="91e82-101">title: "Can't Access this Corporate Application" error when using an Application Proxy application | Microsoft Docs description: How to resolve common access issues with Azure AD Application Proxy applications.</span><span class="sxs-lookup"><span data-stu-id="91e82-101">title: "Can't Access this Corporate Application" error when using an Application Proxy application | Microsoft Docs description: How to resolve common access issues with Azure AD Application Proxy applications.</span></span>
<span data-ttu-id="91e82-102">services: active-directory documentationcenter: '' author: ajamess manager: femila</span><span class="sxs-lookup"><span data-stu-id="91e82-102">services: active-directory documentationcenter: '' author: ajamess manager: femila</span></span>

<span data-ttu-id="91e82-103">ms.assetid: ms.service: active-directory ms.workload: identity ms.tgt_pltfrm: na ms.devlang: na ms.topic: article ms.date: 04/04/2017 ms.author: asteen</span><span class="sxs-lookup"><span data-stu-id="91e82-103">ms.assetid: ms.service: active-directory ms.workload: identity ms.tgt_pltfrm: na ms.devlang: na ms.topic: article ms.date: 04/04/2017 ms.author: asteen</span></span>

---

# <a name="cant-access-this-corporate-application-error-when-using-an-application-proxy-application"></a><span data-ttu-id="91e82-104">"Can't Access this Corporate Application" error when using an Application Proxy application</span><span class="sxs-lookup"><span data-stu-id="91e82-104">"Can't Access this Corporate Application" error when using an Application Proxy application</span></span>

<span data-ttu-id="91e82-105">This article help you to troubleshoot common issues faced when you see a "This corporate app can't be accessed" error on an Azure AD Application Proxy application.</span><span class="sxs-lookup"><span data-stu-id="91e82-105">This article help you to troubleshoot common issues faced when you see a "This corporate app can't be accessed" error on an Azure AD Application Proxy application.</span></span>

## <a name="overview"></a><span data-ttu-id="91e82-106">Overview</span><span class="sxs-lookup"><span data-stu-id="91e82-106">Overview</span></span>
<span data-ttu-id="91e82-107">When you see this error, the page also share a status code.</span><span class="sxs-lookup"><span data-stu-id="91e82-107">When you see this error, the page also share a status code.</span></span> <span data-ttu-id="91e82-108">That code is likely one of the following:</span><span class="sxs-lookup"><span data-stu-id="91e82-108">That code is likely one of the following:</span></span>

-   <span data-ttu-id="91e82-109">**Gateway Timeout**: The Application Proxy service is unable to reach the connector.</span><span class="sxs-lookup"><span data-stu-id="91e82-109">**Gateway Timeout**: The Application Proxy service is unable to reach the connector.</span></span> <span data-ttu-id="91e82-110">This typically indicates a problem with the connector assignment, connector itself, or the networking rules around the connector.</span><span class="sxs-lookup"><span data-stu-id="91e82-110">This typically indicates a problem with the connector assignment, connector itself, or the networking rules around the connector.</span></span>

-   <span data-ttu-id="91e82-111">**Bad Gateway**: The connector is unable to reach the backend application.</span><span class="sxs-lookup"><span data-stu-id="91e82-111">**Bad Gateway**: The connector is unable to reach the backend application.</span></span> <span data-ttu-id="91e82-112">This could indicate a misconfiguration of the application.</span><span class="sxs-lookup"><span data-stu-id="91e82-112">This could indicate a misconfiguration of the application.</span></span>

-   <span data-ttu-id="91e82-113">**Forbidden**: The user is not authorized to access the application.</span><span class="sxs-lookup"><span data-stu-id="91e82-113">**Forbidden**: The user is not authorized to access the application.</span></span> <span data-ttu-id="91e82-114">This can happen either when the user is not assigned to the application in Azure Active Directory, or if on the backend the user does not have permission to access the application.</span><span class="sxs-lookup"><span data-stu-id="91e82-114">This can happen either when the user is not assigned to the application in Azure Active Directory, or if on the backend the user does not have permission to access the application.</span></span>

<span data-ttu-id="91e82-115">To find the code, look at the text at the bottom left of the error message for the “Status Code” field.</span><span class="sxs-lookup"><span data-stu-id="91e82-115">To find the code, look at the text at the bottom left of the error message for the “Status Code” field.</span></span> <span data-ttu-id="91e82-116">Also look for any notes at the very bottom of the page with additional tips.</span><span class="sxs-lookup"><span data-stu-id="91e82-116">Also look for any notes at the very bottom of the page with additional tips.</span></span>

   ![Gateway timeout error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/application-proxy/connection-problem.png)

<span data-ttu-id="91e82-118">For details on how to troubleshoot the root cause of these errors and more details on suggested fixes, see the corresponding section below.</span><span class="sxs-lookup"><span data-stu-id="91e82-118">For details on how to troubleshoot the root cause of these errors and more details on suggested fixes, see the corresponding section below.</span></span>

## <a name="gateway-timeout-errors"></a><span data-ttu-id="91e82-119">Gateway Timeout errors</span><span class="sxs-lookup"><span data-stu-id="91e82-119">Gateway Timeout errors</span></span>

<span data-ttu-id="91e82-120">A gateway timeout occurs when the service tries to reach the connector and is unable to within the timeout window.</span><span class="sxs-lookup"><span data-stu-id="91e82-120">A gateway timeout occurs when the service tries to reach the connector and is unable to within the timeout window.</span></span> <span data-ttu-id="91e82-121">This is typically caused by an application assigned to a Connector Group with no working connectors, or some ports required by the Connector are not open.</span><span class="sxs-lookup"><span data-stu-id="91e82-121">This is typically caused by an application assigned to a Connector Group with no working connectors, or some ports required by the Connector are not open.</span></span>


## <a name="bad-gateway-errors"></a><span data-ttu-id="91e82-122">Bad Gateway errors</span><span class="sxs-lookup"><span data-stu-id="91e82-122">Bad Gateway errors</span></span>

<span data-ttu-id="91e82-123">A bad gateway error indicates that the connector is unable to reach the backend application.</span><span class="sxs-lookup"><span data-stu-id="91e82-123">A bad gateway error indicates that the connector is unable to reach the backend application.</span></span> <span data-ttu-id="91e82-124">make sure that you have published the correct application.</span><span class="sxs-lookup"><span data-stu-id="91e82-124">make sure that you have published the correct application.</span></span> <span data-ttu-id="91e82-125">Common mistakes that cause this error:</span><span class="sxs-lookup"><span data-stu-id="91e82-125">Common mistakes that cause this error:</span></span>

-   <span data-ttu-id="91e82-126">A typo or mistake in the internal URL</span><span class="sxs-lookup"><span data-stu-id="91e82-126">A typo or mistake in the internal URL</span></span>

-   <span data-ttu-id="91e82-127">Not publishing the root of the application.</span><span class="sxs-lookup"><span data-stu-id="91e82-127">Not publishing the root of the application.</span></span> <span data-ttu-id="91e82-128">For example, publishing <http://expenses/reimbursement> but trying to access <http://expenses></span><span class="sxs-lookup"><span data-stu-id="91e82-128">For example, publishing <http://expenses/reimbursement> but trying to access <http://expenses></span></span>

-   <span data-ttu-id="91e82-129">Problems with the Kerberos Constrained Delegation (KCD) configuration</span><span class="sxs-lookup"><span data-stu-id="91e82-129">Problems with the Kerberos Constrained Delegation (KCD) configuration</span></span>

-   <span data-ttu-id="91e82-130">Problems with the backend application</span><span class="sxs-lookup"><span data-stu-id="91e82-130">Problems with the backend application</span></span>

## <a name="forbidden-errors"></a><span data-ttu-id="91e82-131">Forbidden errors</span><span class="sxs-lookup"><span data-stu-id="91e82-131">Forbidden errors</span></span>

<span data-ttu-id="91e82-132">If you see a forbidden error, the user has not been assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="91e82-132">If you see a forbidden error, the user has not been assigned to the application.</span></span> <span data-ttu-id="91e82-133">This could be either in Azure Active Directory or on the backend application.</span><span class="sxs-lookup"><span data-stu-id="91e82-133">This could be either in Azure Active Directory or on the backend application.</span></span>

<span data-ttu-id="91e82-134">To learn how to assign users to the application in Azure, see the [configuration documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal#add-a-test-user).</span><span class="sxs-lookup"><span data-stu-id="91e82-134">To learn how to assign users to the application in Azure, see the [configuration documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal#add-a-test-user).</span></span>

<span data-ttu-id="91e82-135">If you confirm the user is assigned to the application in Azure, check the user configuration in the backend application.</span><span class="sxs-lookup"><span data-stu-id="91e82-135">If you confirm the user is assigned to the application in Azure, check the user configuration in the backend application.</span></span> <span data-ttu-id="91e82-136">If you are using Kerberos Constrained Delegation/Integrated Windows Authentication, you can see our KCD Troubleshoot page for some guidelines.</span><span class="sxs-lookup"><span data-stu-id="91e82-136">If you are using Kerberos Constrained Delegation/Integrated Windows Authentication, you can see our KCD Troubleshoot page for some guidelines.</span></span>

## <a name="check-the-applications-internal-url"></a><span data-ttu-id="91e82-137">Check the application's internal URL</span><span class="sxs-lookup"><span data-stu-id="91e82-137">Check the application's internal URL</span></span>

<span data-ttu-id="91e82-138">As a first quick step, double check check and fix the internal URL by opening the application through **Enterprise Applications**, then selecting the **Application Proxy** menu.</span><span class="sxs-lookup"><span data-stu-id="91e82-138">As a first quick step, double check check and fix the internal URL by opening the application through **Enterprise Applications**, then selecting the **Application Proxy** menu.</span></span> <span data-ttu-id="91e82-139">Verify this is the correct internal URL, the one used from your on-prem network to access the application.</span><span class="sxs-lookup"><span data-stu-id="91e82-139">Verify this is the correct internal URL, the one used from your on-prem network to access the application.</span></span>

## <a name="check-the-application-is-assigned-to-a-working-connector-group"></a><span data-ttu-id="91e82-140">Check the application is assigned to a working Connector Group</span><span class="sxs-lookup"><span data-stu-id="91e82-140">Check the application is assigned to a working Connector Group</span></span>

<span data-ttu-id="91e82-141">To verify the application is assigned to a working Connector Group:</span><span class="sxs-lookup"><span data-stu-id="91e82-141">To verify the application is assigned to a working Connector Group:</span></span>

1.  <span data-ttu-id="91e82-142">Open the application in the portal by going to **Azure Active Directory**, clicking on **Enterprise Applications**, then **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="91e82-142">Open the application in the portal by going to **Azure Active Directory**, clicking on **Enterprise Applications**, then **All Applications.**</span></span> <span data-ttu-id="91e82-143">Open the application, then select **Application Proxy** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="91e82-143">Open the application, then select **Application Proxy** from the left menu.</span></span>

2.  <span data-ttu-id="91e82-144">Look at the Connector Group field.</span><span class="sxs-lookup"><span data-stu-id="91e82-144">Look at the Connector Group field.</span></span> <span data-ttu-id="91e82-145">If there are no active connectors in the group, you see a warning.</span><span class="sxs-lookup"><span data-stu-id="91e82-145">If there are no active connectors in the group, you see a warning.</span></span> <span data-ttu-id="91e82-146">If you don’t see any warnings, move on to “verify all required ports are whitelisted”.</span><span class="sxs-lookup"><span data-stu-id="91e82-146">If you don’t see any warnings, move on to “verify all required ports are whitelisted”.</span></span>

3.  <span data-ttu-id="91e82-147">If this is the wrong Connector Group, use the drop down to select the correct group, and confirm you no longer see any warnings.</span><span class="sxs-lookup"><span data-stu-id="91e82-147">If this is the wrong Connector Group, use the drop down to select the correct group, and confirm you no longer see any warnings.</span></span> <span data-ttu-id="91e82-148">If this is the intended Connector Group, click the warning message to open the page with Connector management.</span><span class="sxs-lookup"><span data-stu-id="91e82-148">If this is the intended Connector Group, click the warning message to open the page with Connector management.</span></span>

4.  <span data-ttu-id="91e82-149">From here, there are a few ways to drill in further:</span><span class="sxs-lookup"><span data-stu-id="91e82-149">From here, there are a few ways to drill in further:</span></span>

  * <span data-ttu-id="91e82-150">Move an active Connector into the group: If you have an active Connector that should belong to this group and has line of sight to the target backend application, you can move the Connector into the assigned group.</span><span class="sxs-lookup"><span data-stu-id="91e82-150">Move an active Connector into the group: If you have an active Connector that should belong to this group and has line of sight to the target backend application, you can move the Connector into the assigned group.</span></span> <span data-ttu-id="91e82-151">To do so, click the Connector.</span><span class="sxs-lookup"><span data-stu-id="91e82-151">To do so, click the Connector.</span></span> <span data-ttu-id="91e82-152">In the “Connector Group” field, use the drop-down to select the correct group, and click save.</span><span class="sxs-lookup"><span data-stu-id="91e82-152">In the “Connector Group” field, use the drop-down to select the correct group, and click save.</span></span>

  * <span data-ttu-id="91e82-153">Download a new Connector for that group: From this page, you can get the link to [download a new Connector](https://download.msappproxy.net/Subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/Connector/Download).</span><span class="sxs-lookup"><span data-stu-id="91e82-153">Download a new Connector for that group: From this page, you can get the link to [download a new Connector](https://download.msappproxy.net/Subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/Connector/Download).</span></span> <span data-ttu-id="91e82-154">The Connector needs to be installed on a machine with direct line of sight to the backend application, and is typically placed on the same server as the application.</span><span class="sxs-lookup"><span data-stu-id="91e82-154">The Connector needs to be installed on a machine with direct line of sight to the backend application, and is typically placed on the same server as the application.</span></span> <span data-ttu-id="91e82-155">Use the download Connector link to download a connector onto the target machine.</span><span class="sxs-lookup"><span data-stu-id="91e82-155">Use the download Connector link to download a connector onto the target machine.</span></span> <span data-ttu-id="91e82-156">Next, click the Connector, and use the “Connector Group” drop-down to make sure it belongs to the right group.</span><span class="sxs-lookup"><span data-stu-id="91e82-156">Next, click the Connector, and use the “Connector Group” drop-down to make sure it belongs to the right group.</span></span>

  * <span data-ttu-id="91e82-157">Investigate an inactive Connector: If a connector shows as inactive, it is unable to reach the service.</span><span class="sxs-lookup"><span data-stu-id="91e82-157">Investigate an inactive Connector: If a connector shows as inactive, it is unable to reach the service.</span></span> <span data-ttu-id="91e82-158">This is typically due to some required ports being blocked.</span><span class="sxs-lookup"><span data-stu-id="91e82-158">This is typically due to some required ports being blocked.</span></span> <span data-ttu-id="91e82-159">To solve this issue, move on to “verify all required ports are whitelisted”.</span><span class="sxs-lookup"><span data-stu-id="91e82-159">To solve this issue, move on to “verify all required ports are whitelisted”.</span></span>

<span data-ttu-id="91e82-160">After using these steps to ensure the application is assigned to a group with working Connectors, test the application again.</span><span class="sxs-lookup"><span data-stu-id="91e82-160">After using these steps to ensure the application is assigned to a group with working Connectors, test the application again.</span></span> <span data-ttu-id="91e82-161">If it is still not working, continue to the next section.</span><span class="sxs-lookup"><span data-stu-id="91e82-161">If it is still not working, continue to the next section.</span></span>

## <a name="check-all-required-ports-are-whitelisted"></a><span data-ttu-id="91e82-162">Check all required ports are whitelisted</span><span class="sxs-lookup"><span data-stu-id="91e82-162">Check all required ports are whitelisted</span></span>

<span data-ttu-id="91e82-163">To verify that all required ports are open, see our documentation on opening ports.</span><span class="sxs-lookup"><span data-stu-id="91e82-163">To verify that all required ports are open, see our documentation on opening ports.</span></span> <span data-ttu-id="91e82-164">If all the required ports are open, move to the next section.</span><span class="sxs-lookup"><span data-stu-id="91e82-164">If all the required ports are open, move to the next section.</span></span>

## <a name="check-for-other-connector-errors"></a><span data-ttu-id="91e82-165">Check for other Connector Errors</span><span class="sxs-lookup"><span data-stu-id="91e82-165">Check for other Connector Errors</span></span>

<span data-ttu-id="91e82-166">If none of the above resolve the issue, the next step is to look for issues or errors with the Connector itself.</span><span class="sxs-lookup"><span data-stu-id="91e82-166">If none of the above resolve the issue, the next step is to look for issues or errors with the Connector itself.</span></span> <span data-ttu-id="91e82-167">You can see some common errors in the [Troubleshoot document](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors).</span><span class="sxs-lookup"><span data-stu-id="91e82-167">You can see some common errors in the [Troubleshoot document](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors).</span></span> 

<span data-ttu-id="91e82-168">You can also look directly at the Connector logs to identify any errors.</span><span class="sxs-lookup"><span data-stu-id="91e82-168">You can also look directly at the Connector logs to identify any errors.</span></span> <span data-ttu-id="91e82-169">Many of our error messages be able to share more specific recommendations for fixes.</span><span class="sxs-lookup"><span data-stu-id="91e82-169">Many of our error messages be able to share more specific recommendations for fixes.</span></span> <span data-ttu-id="91e82-170">To learn how to view the logs, see [our connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).</span><span class="sxs-lookup"><span data-stu-id="91e82-170">To learn how to view the logs, see [our connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).</span></span>

## <a name="additional-resolutions"></a><span data-ttu-id="91e82-171">Additional Resolutions</span><span class="sxs-lookup"><span data-stu-id="91e82-171">Additional Resolutions</span></span>

<span data-ttu-id="91e82-172">If the above didn’t fix the problem, there are a few different possible causes.</span><span class="sxs-lookup"><span data-stu-id="91e82-172">If the above didn’t fix the problem, there are a few different possible causes.</span></span> <span data-ttu-id="91e82-173">To identify the issue:</span><span class="sxs-lookup"><span data-stu-id="91e82-173">To identify the issue:</span></span>

<span data-ttu-id="91e82-174">If your application is configured to use Integrated Windows Authentication (IWA), test the application without single sign-on.</span><span class="sxs-lookup"><span data-stu-id="91e82-174">If your application is configured to use Integrated Windows Authentication (IWA), test the application without single sign-on.</span></span> <span data-ttu-id="91e82-175">If not, move to the next paragraph.</span><span class="sxs-lookup"><span data-stu-id="91e82-175">If not, move to the next paragraph.</span></span> <span data-ttu-id="91e82-176">To check the application without single sign-on, open your application through **Enterprise Applications,** and go to the **Single Sign-On** menu.</span><span class="sxs-lookup"><span data-stu-id="91e82-176">To check the application without single sign-on, open your application through **Enterprise Applications,** and go to the **Single Sign-On** menu.</span></span> <span data-ttu-id="91e82-177">Change the drop down from “Integrated Windows Authentication” to “Azure AD single sign-on disabled”.</span><span class="sxs-lookup"><span data-stu-id="91e82-177">Change the drop down from “Integrated Windows Authentication” to “Azure AD single sign-on disabled”.</span></span> 

<span data-ttu-id="91e82-178">Now open a browser and try to access the application again.</span><span class="sxs-lookup"><span data-stu-id="91e82-178">Now open a browser and try to access the application again.</span></span> <span data-ttu-id="91e82-179">You should be prompted for authentication and get into the application.</span><span class="sxs-lookup"><span data-stu-id="91e82-179">You should be prompted for authentication and get into the application.</span></span> <span data-ttu-id="91e82-180">If this works, the problem is with the Kerberos Constrained Delegation (KCD) configuration that enables the single sign-on.</span><span class="sxs-lookup"><span data-stu-id="91e82-180">If this works, the problem is with the Kerberos Constrained Delegation (KCD) configuration that enables the single sign-on.</span></span> <span data-ttu-id="91e82-181">see the KCD Troubleshoot page.</span><span class="sxs-lookup"><span data-stu-id="91e82-181">see the KCD Troubleshoot page.</span></span>

<span data-ttu-id="91e82-182">If you continue to see the error, go to the machine where the Connector is installed, open a browser and attempt to reach the internal URL used for the application.</span><span class="sxs-lookup"><span data-stu-id="91e82-182">If you continue to see the error, go to the machine where the Connector is installed, open a browser and attempt to reach the internal URL used for the application.</span></span> <span data-ttu-id="91e82-183">The Connector acts like another client from the same machine.</span><span class="sxs-lookup"><span data-stu-id="91e82-183">The Connector acts like another client from the same machine.</span></span> <span data-ttu-id="91e82-184">If you can’t reach the application, investigate why that machine is unable to reach the application, or use a connector on a server that is able to access the application.</span><span class="sxs-lookup"><span data-stu-id="91e82-184">If you can’t reach the application, investigate why that machine is unable to reach the application, or use a connector on a server that is able to access the application.</span></span>

<span data-ttu-id="91e82-185">If you can reach the application from that machine, to look for issues or errors with the Connector itself.</span><span class="sxs-lookup"><span data-stu-id="91e82-185">If you can reach the application from that machine, to look for issues or errors with the Connector itself.</span></span> <span data-ttu-id="91e82-186">You can see some common errors in the [Troubleshoot document](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors).</span><span class="sxs-lookup"><span data-stu-id="91e82-186">You can see some common errors in the [Troubleshoot document](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors).</span></span> <span data-ttu-id="91e82-187">You can also look directly at the Connector logs to identify any errors.</span><span class="sxs-lookup"><span data-stu-id="91e82-187">You can also look directly at the Connector logs to identify any errors.</span></span> <span data-ttu-id="91e82-188">Many of our error messages be able to share more specific recommendations for fixes.</span><span class="sxs-lookup"><span data-stu-id="91e82-188">Many of our error messages be able to share more specific recommendations for fixes.</span></span> <span data-ttu-id="91e82-189">To learn how to view the logs, see [our connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).</span><span class="sxs-lookup"><span data-stu-id="91e82-189">To learn how to view the logs, see [our connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).</span></span>

## <a name="next-steps"></a><span data-ttu-id="91e82-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="91e82-190">Next steps</span></span>
[<span data-ttu-id="91e82-191">Understand Azure AD Application Proxy connectors</span><span class="sxs-lookup"><span data-stu-id="91e82-191">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
