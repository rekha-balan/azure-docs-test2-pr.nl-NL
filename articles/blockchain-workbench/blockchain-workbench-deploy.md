---
title: Deploy Azure Blockchain Workbench
description: How to deploy Azure Blockchain Workbench
services: azure-blockchain
keywords: ''
author: PatAltimore
ms.author: patricka
ms.date: 7/13/2018
ms.topic: article
ms.service: azure-blockchain
ms.reviewer: zeyadr
manager: femila
ms.openlocfilehash: 1a0bc85063a80854ff6b970b0a57a991acfb3750
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864612"
---
# <a name="deploy-azure-blockchain-workbench"></a><span data-ttu-id="3b7b1-103">Deploy Azure Blockchain Workbench</span><span class="sxs-lookup"><span data-stu-id="3b7b1-103">Deploy Azure Blockchain Workbench</span></span>

<span data-ttu-id="3b7b1-104">Azure Blockchain Workbench is deployed using a solution template in the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-104">Azure Blockchain Workbench is deployed using a solution template in the Azure Marketplace.</span></span> <span data-ttu-id="3b7b1-105">The template simplifies the deployment of components needed to create blockchain applications.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-105">The template simplifies the deployment of components needed to create blockchain applications.</span></span> <span data-ttu-id="3b7b1-106">Once deployed, Blockchain Workbench provides access to client apps to create and manage users and blockchain applications.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-106">Once deployed, Blockchain Workbench provides access to client apps to create and manage users and blockchain applications.</span></span>

<span data-ttu-id="3b7b1-107">For more information about the components of Blockchain Workbench, see [Azure Blockchain Workbench architecture](blockchain-workbench-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="3b7b1-107">For more information about the components of Blockchain Workbench, see [Azure Blockchain Workbench architecture](blockchain-workbench-architecture.md).</span></span>

## <a name="prepare-for-deployment"></a><span data-ttu-id="3b7b1-108">Prepare for deployment</span><span class="sxs-lookup"><span data-stu-id="3b7b1-108">Prepare for deployment</span></span>

<span data-ttu-id="3b7b1-109">Blockchain Workbench allows you to deploy a blockchain ledger along with a set of relevant Azure services most often used to build a blockchain-based application.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-109">Blockchain Workbench allows you to deploy a blockchain ledger along with a set of relevant Azure services most often used to build a blockchain-based application.</span></span> <span data-ttu-id="3b7b1-110">Deploying Blockchain Workbench results in the following Azure services being provisioned within a resource group in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-110">Deploying Blockchain Workbench results in the following Azure services being provisioned within a resource group in your Azure subscription.</span></span>

* <span data-ttu-id="3b7b1-111">1 Event Grid Topic</span><span class="sxs-lookup"><span data-stu-id="3b7b1-111">1 Event Grid Topic</span></span>
* <span data-ttu-id="3b7b1-112">1 Service Bus Namespace</span><span class="sxs-lookup"><span data-stu-id="3b7b1-112">1 Service Bus Namespace</span></span>
* <span data-ttu-id="3b7b1-113">1 Application Insights</span><span class="sxs-lookup"><span data-stu-id="3b7b1-113">1 Application Insights</span></span>
* <span data-ttu-id="3b7b1-114">1 SQL Database (Standard S0)</span><span class="sxs-lookup"><span data-stu-id="3b7b1-114">1 SQL Database (Standard S0)</span></span>
* <span data-ttu-id="3b7b1-115">2 App Services (Standard)</span><span class="sxs-lookup"><span data-stu-id="3b7b1-115">2 App Services (Standard)</span></span>
* <span data-ttu-id="3b7b1-116">2 Azure Key Vaults</span><span class="sxs-lookup"><span data-stu-id="3b7b1-116">2 Azure Key Vaults</span></span>
* <span data-ttu-id="3b7b1-117">2 Azure Storage accounts (Standard LRS)</span><span class="sxs-lookup"><span data-stu-id="3b7b1-117">2 Azure Storage accounts (Standard LRS)</span></span>
* <span data-ttu-id="3b7b1-118">2 Virtual machine scale sets (for validator and worker nodes)</span><span class="sxs-lookup"><span data-stu-id="3b7b1-118">2 Virtual machine scale sets (for validator and worker nodes)</span></span>
* <span data-ttu-id="3b7b1-119">2 Virtual Networks (including load balancer, network security group, and public IP address for each virtual network)</span><span class="sxs-lookup"><span data-stu-id="3b7b1-119">2 Virtual Networks (including load balancer, network security group, and public IP address for each virtual network)</span></span>
* <span data-ttu-id="3b7b1-120">Optional: Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="3b7b1-120">Optional: Azure Monitor</span></span>

<span data-ttu-id="3b7b1-121">The following is an example deployment created in **myblockchain** resource group.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-121">The following is an example deployment created in **myblockchain** resource group.</span></span>

![Example deployment](media/blockchain-workbench-deploy/example-deployment.png)

<span data-ttu-id="3b7b1-123">The cost of Blockchain Workbench is an aggregate of the cost of the underlying Azure services.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-123">The cost of Blockchain Workbench is an aggregate of the cost of the underlying Azure services.</span></span> <span data-ttu-id="3b7b1-124">Pricing information for Azure services can be calculated using the [pricing calculator](https://azure.microsoft.com/pricing/calculator/).</span><span class="sxs-lookup"><span data-stu-id="3b7b1-124">Pricing information for Azure services can be calculated using the [pricing calculator](https://azure.microsoft.com/pricing/calculator/).</span></span>

<span data-ttu-id="3b7b1-125">Azure Blockchain Workbench requires several prerequisites prior to the deployment.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-125">Azure Blockchain Workbench requires several prerequisites prior to the deployment.</span></span> <span data-ttu-id="3b7b1-126">The prerequisites include Azure AD configuration and application registrations.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-126">The prerequisites include Azure AD configuration and application registrations.</span></span>

### <a name="blockchain-workbench-api-app-registration"></a><span data-ttu-id="3b7b1-127">Blockchain Workbench API app registration</span><span class="sxs-lookup"><span data-stu-id="3b7b1-127">Blockchain Workbench API app registration</span></span>

<span data-ttu-id="3b7b1-128">Blockchain Workbench deployment requires registration of an Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-128">Blockchain Workbench deployment requires registration of an Azure AD application.</span></span> <span data-ttu-id="3b7b1-129">You need an Azure Active Directory (Azure AD) tenant to register the app.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-129">You need an Azure Active Directory (Azure AD) tenant to register the app.</span></span> <span data-ttu-id="3b7b1-130">You can use an existing tenant or create a new tenant.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-130">You can use an existing tenant or create a new tenant.</span></span> <span data-ttu-id="3b7b1-131">If you are using an existing Azure AD tenant, you need sufficient permissions to register applications and grant Graph API permissions within an Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-131">If you are using an existing Azure AD tenant, you need sufficient permissions to register applications and grant Graph API permissions within an Azure AD tenant.</span></span> <span data-ttu-id="3b7b1-132">If you do not have sufficient permissions in an existing Azure AD tenant create a new tenant.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-132">If you do not have sufficient permissions in an existing Azure AD tenant create a new tenant.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3b7b1-133">Workbench does not have to be deployed in the same tenant as the one you are using to register an Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-133">Workbench does not have to be deployed in the same tenant as the one you are using to register an Azure AD application.</span></span> <span data-ttu-id="3b7b1-134">Workbench must be deployed in a tenant where you have sufficient permissions to deploy resources.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-134">Workbench must be deployed in a tenant where you have sufficient permissions to deploy resources.</span></span> <span data-ttu-id="3b7b1-135">For more information on Azure AD tenants, see [How to get an Active Directory tenant](../active-directory/develop/quickstart-create-new-tenant.md) and [Integrating applications with Azure Active Directory](../active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad.md).</span><span class="sxs-lookup"><span data-stu-id="3b7b1-135">For more information on Azure AD tenants, see [How to get an Active Directory tenant](../active-directory/develop/quickstart-create-new-tenant.md) and [Integrating applications with Azure Active Directory](../active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad.md).</span></span>

1. <span data-ttu-id="3b7b1-136">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3b7b1-136">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3b7b1-137">Select your account in the top right corner, and switch to the desired Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-137">Select your account in the top right corner, and switch to the desired Azure AD tenant.</span></span> <span data-ttu-id="3b7b1-138">The tenant should be the subscription admin's tenant of the subscription where Workbench is deployed and you have sufficient permissions to register applications.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-138">The tenant should be the subscription admin's tenant of the subscription where Workbench is deployed and you have sufficient permissions to register applications.</span></span>
3. <span data-ttu-id="3b7b1-139">In the left-hand navigation pane, select the **Azure Active Directory** service.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-139">In the left-hand navigation pane, select the **Azure Active Directory** service.</span></span> <span data-ttu-id="3b7b1-140">Select **App registrations** > **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-140">Select **App registrations** > **New application registration**.</span></span>

    ![App registration](media/blockchain-workbench-deploy/app-registration.png)

4. <span data-ttu-id="3b7b1-142">Provide a **Name** and **Sign-on URL** for the application.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-142">Provide a **Name** and **Sign-on URL** for the application.</span></span> <span data-ttu-id="3b7b1-143">You can use placeholder values since the values are changed during the deployment.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-143">You can use placeholder values since the values are changed during the deployment.</span></span> 

    ![Create app registration](media/blockchain-workbench-deploy/app-registration-create.png)

    |<span data-ttu-id="3b7b1-145">Setting</span><span class="sxs-lookup"><span data-stu-id="3b7b1-145">Setting</span></span>  | <span data-ttu-id="3b7b1-146">Value</span><span class="sxs-lookup"><span data-stu-id="3b7b1-146">Value</span></span>  |
    |---------|---------|
    |<span data-ttu-id="3b7b1-147">Name</span><span class="sxs-lookup"><span data-stu-id="3b7b1-147">Name</span></span> | `Blockchain API` |
    |<span data-ttu-id="3b7b1-148">Application type</span><span class="sxs-lookup"><span data-stu-id="3b7b1-148">Application type</span></span> |<span data-ttu-id="3b7b1-149">Web app / API</span><span class="sxs-lookup"><span data-stu-id="3b7b1-149">Web app / API</span></span>|
    |<span data-ttu-id="3b7b1-150">Sign-on URL</span><span class="sxs-lookup"><span data-stu-id="3b7b1-150">Sign-on URL</span></span> | `https://blockchainapi` |

5. <span data-ttu-id="3b7b1-151">Select **Create** to register the Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-151">Select **Create** to register the Azure AD application.</span></span>

### <a name="modify-application-manifest"></a><span data-ttu-id="3b7b1-152">Modify application manifest</span><span class="sxs-lookup"><span data-stu-id="3b7b1-152">Modify application manifest</span></span>

<span data-ttu-id="3b7b1-153">Next, you need to modify the application manifest to use application roles within Azure AD to specify Blockchain Workbench administrators.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-153">Next, you need to modify the application manifest to use application roles within Azure AD to specify Blockchain Workbench administrators.</span></span>  <span data-ttu-id="3b7b1-154">For more information about application manifests, see [Azure Active Directory application manifest](../active-directory/develop/reference-app-manifest.md).</span><span class="sxs-lookup"><span data-stu-id="3b7b1-154">For more information about application manifests, see [Azure Active Directory application manifest](../active-directory/develop/reference-app-manifest.md).</span></span>

1. <span data-ttu-id="3b7b1-155">For the application you registered, select **Manifest** in the registered application details pane.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-155">For the application you registered, select **Manifest** in the registered application details pane.</span></span>
2. <span data-ttu-id="3b7b1-156">Generate a GUID.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-156">Generate a GUID.</span></span> <span data-ttu-id="3b7b1-157">You can generate a GUID using the PowerShell command [guid] :: NewGuid () or New-GUID cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-157">You can generate a GUID using the PowerShell command [guid] :: NewGuid () or New-GUID cmdlet.</span></span> <span data-ttu-id="3b7b1-158">Another option is to use a GUID generator website.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-158">Another option is to use a GUID generator website.</span></span>
3. <span data-ttu-id="3b7b1-159">You are going to update the **appRoles** section of the manifest.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-159">You are going to update the **appRoles** section of the manifest.</span></span> <span data-ttu-id="3b7b1-160">In the Edit manifest pane, select **Edit** and replace `"appRoles": []` with the provided JSON.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-160">In the Edit manifest pane, select **Edit** and replace `"appRoles": []` with the provided JSON.</span></span> <span data-ttu-id="3b7b1-161">Be sure to replace the value for the **id** field with the GUID you generated.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-161">Be sure to replace the value for the **id** field with the GUID you generated.</span></span> 

    ``` json
    "appRoles": [
         {
           "allowedMemberTypes": [
             "User",
             "Application"
           ],
           "displayName": "Administrator",
           "id": "<A unique GUID>",
           "isEnabled": true,
           "description": "Blockchain Workbench administrator role allows creation of applications, user to role assignments, etc.",
           "value": "Administrator"
         }
       ],
    ```

    ![Edit manifest](media/blockchain-workbench-deploy/edit-manifest.png)

    > [!IMPORTANT]
    > <span data-ttu-id="3b7b1-163">The value **Administrator** is needed to identify Blockchain Workbench administrators.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-163">The value **Administrator** is needed to identify Blockchain Workbench administrators.</span></span>

4.  <span data-ttu-id="3b7b1-164">Click **Save** to save the application manifest changes.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-164">Click **Save** to save the application manifest changes.</span></span>

### <a name="add-graph-api-required-permissions"></a><span data-ttu-id="3b7b1-165">Add Graph API required permissions</span><span class="sxs-lookup"><span data-stu-id="3b7b1-165">Add Graph API required permissions</span></span>

<span data-ttu-id="3b7b1-166">The API application needs to request permission from the user to access the directory.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-166">The API application needs to request permission from the user to access the directory.</span></span> <span data-ttu-id="3b7b1-167">Set the following required permission for the API application:</span><span class="sxs-lookup"><span data-stu-id="3b7b1-167">Set the following required permission for the API application:</span></span>

1. <span data-ttu-id="3b7b1-168">In the Blockchain API app registration, select **Settings > Required permissions > Select an API > Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-168">In the Blockchain API app registration, select **Settings > Required permissions > Select an API > Microsoft Graph**.</span></span>

    ![Select an API](media/blockchain-workbench-deploy/client-app-select-api.png)

    <span data-ttu-id="3b7b1-170">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-170">Click **Select**.</span></span>

2. <span data-ttu-id="3b7b1-171">In **Enable Access** under **Application permissions**, choose **Read all users' full profiles**.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-171">In **Enable Access** under **Application permissions**, choose **Read all users' full profiles**.</span></span>

    ![Enable access](media/blockchain-workbench-deploy/client-app-read-perms.png)

    <span data-ttu-id="3b7b1-173">Click **Select** then click **Done**.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-173">Click **Select** then click **Done**.</span></span>

3. <span data-ttu-id="3b7b1-174">In **Required permissions**, select **Grant Permissions** then select **Yes** for the verification prompt.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-174">In **Required permissions**, select **Grant Permissions** then select **Yes** for the verification prompt.</span></span>

   ![Grant permissions](media/blockchain-workbench-deploy/client-app-grant-permissions.png)

   <span data-ttu-id="3b7b1-176">Granting permission allows Blockchain Workbench to access users in the directory.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-176">Granting permission allows Blockchain Workbench to access users in the directory.</span></span> <span data-ttu-id="3b7b1-177">The read permission is required to search and add members to Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-177">The read permission is required to search and add members to Blockchain Workbench.</span></span>

### <a name="add-graph-api-key-to-application"></a><span data-ttu-id="3b7b1-178">Add Graph API key to application</span><span class="sxs-lookup"><span data-stu-id="3b7b1-178">Add Graph API key to application</span></span>

<span data-ttu-id="3b7b1-179">Blockchain Workbench uses Azure AD as the main identity management system for users interacting with blockchain applications.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-179">Blockchain Workbench uses Azure AD as the main identity management system for users interacting with blockchain applications.</span></span> <span data-ttu-id="3b7b1-180">In order for Blockchain Workbench to access Azure AD and retrieve user information, such as names and emails, you need to add an access key.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-180">In order for Blockchain Workbench to access Azure AD and retrieve user information, such as names and emails, you need to add an access key.</span></span> <span data-ttu-id="3b7b1-181">Blockchain Workbench uses the key to authenticate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-181">Blockchain Workbench uses the key to authenticate with Azure AD.</span></span>

1. <span data-ttu-id="3b7b1-182">For the application you registered, select **Settings** in the registered application details pane.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-182">For the application you registered, select **Settings** in the registered application details pane.</span></span>
2. <span data-ttu-id="3b7b1-183">Select **Keys**.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-183">Select **Keys**.</span></span>
3. <span data-ttu-id="3b7b1-184">Add a new key by specifying a key **description** and choosing **expires** duration value.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-184">Add a new key by specifying a key **description** and choosing **expires** duration value.</span></span> 

    ![Create key](media/blockchain-workbench-deploy/app-key-create.png)

    |<span data-ttu-id="3b7b1-186">Setting</span><span class="sxs-lookup"><span data-stu-id="3b7b1-186">Setting</span></span>  | <span data-ttu-id="3b7b1-187">Value</span><span class="sxs-lookup"><span data-stu-id="3b7b1-187">Value</span></span>  |
    |---------|---------|
    | <span data-ttu-id="3b7b1-188">Description</span><span class="sxs-lookup"><span data-stu-id="3b7b1-188">Description</span></span> | `Service` |
    | <span data-ttu-id="3b7b1-189">Expires</span><span class="sxs-lookup"><span data-stu-id="3b7b1-189">Expires</span></span> | <span data-ttu-id="3b7b1-190">Choose an expiration duration</span><span class="sxs-lookup"><span data-stu-id="3b7b1-190">Choose an expiration duration</span></span> |

4. <span data-ttu-id="3b7b1-191">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-191">Select **Save**.</span></span> 
5. <span data-ttu-id="3b7b1-192">Copy the value of the key and store it for later.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-192">Copy the value of the key and store it for later.</span></span> <span data-ttu-id="3b7b1-193">You need it for deployment.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-193">You need it for deployment.</span></span>

    > [!IMPORTANT]
    >  <span data-ttu-id="3b7b1-194">If you don't save the key for the deployment, you will need to generate a new key.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-194">If you don't save the key for the deployment, you will need to generate a new key.</span></span> <span data-ttu-id="3b7b1-195">You can't retrieve the key value from the portal later.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-195">You can't retrieve the key value from the portal later.</span></span>

### <a name="get-application-id"></a><span data-ttu-id="3b7b1-196">Get application ID</span><span class="sxs-lookup"><span data-stu-id="3b7b1-196">Get application ID</span></span>

<span data-ttu-id="3b7b1-197">The application ID and tenant information are required for deployment.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-197">The application ID and tenant information are required for deployment.</span></span> <span data-ttu-id="3b7b1-198">Collect and store the information for use during deployment.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-198">Collect and store the information for use during deployment.</span></span>

1. <span data-ttu-id="3b7b1-199">For the application you registered, select **Settings** > **Properties**.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-199">For the application you registered, select **Settings** > **Properties**.</span></span>
2.  <span data-ttu-id="3b7b1-200">In the **Properties** pane, copy and store the following values for later use during deployment.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-200">In the **Properties** pane, copy and store the following values for later use during deployment.</span></span>

    ![API app properties](media/blockchain-workbench-deploy/app-properties.png)

    | <span data-ttu-id="3b7b1-202">Setting to store</span><span class="sxs-lookup"><span data-stu-id="3b7b1-202">Setting to store</span></span>  | <span data-ttu-id="3b7b1-203">Use in deployment</span><span class="sxs-lookup"><span data-stu-id="3b7b1-203">Use in deployment</span></span> |
    |------------------|-------------------|
    | <span data-ttu-id="3b7b1-204">Application ID</span><span class="sxs-lookup"><span data-stu-id="3b7b1-204">Application ID</span></span> | <span data-ttu-id="3b7b1-205">Azure Active Directory setup > Application ID</span><span class="sxs-lookup"><span data-stu-id="3b7b1-205">Azure Active Directory setup > Application ID</span></span> |

### <a name="get-tenant-domain-name"></a><span data-ttu-id="3b7b1-206">Get tenant domain name</span><span class="sxs-lookup"><span data-stu-id="3b7b1-206">Get tenant domain name</span></span>

<span data-ttu-id="3b7b1-207">Collect and store the Active Directory tenant domain name where the applications are registered.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-207">Collect and store the Active Directory tenant domain name where the applications are registered.</span></span> 

<span data-ttu-id="3b7b1-208">In the left-hand navigation pane, select the **Azure Active Directory** service.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-208">In the left-hand navigation pane, select the **Azure Active Directory** service.</span></span> <span data-ttu-id="3b7b1-209">Select **Custom domain names**.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-209">Select **Custom domain names**.</span></span> <span data-ttu-id="3b7b1-210">Copy and store the domain name.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-210">Copy and store the domain name.</span></span>

![Domain name](media/blockchain-workbench-deploy/domain-name.png)

## <a name="deploy-blockchain-workbench"></a><span data-ttu-id="3b7b1-212">Deploy Blockchain Workbench</span><span class="sxs-lookup"><span data-stu-id="3b7b1-212">Deploy Blockchain Workbench</span></span>

<span data-ttu-id="3b7b1-213">Once the prerequisite steps have been completed, you are ready to deploy the Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-213">Once the prerequisite steps have been completed, you are ready to deploy the Blockchain Workbench.</span></span> <span data-ttu-id="3b7b1-214">The following sections outline how to deploy the framework.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-214">The following sections outline how to deploy the framework.</span></span>

1.  <span data-ttu-id="3b7b1-215">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3b7b1-215">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="3b7b1-216">Select your account in the top right corner, and switch to the desired Azure AD tenant where you want to deploy Azure Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-216">Select your account in the top right corner, and switch to the desired Azure AD tenant where you want to deploy Azure Blockchain Workbench.</span></span>
3.  <span data-ttu-id="3b7b1-217">In the left pane, select **Create a resource**.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-217">In the left pane, select **Create a resource**.</span></span> <span data-ttu-id="3b7b1-218">Search for `Azure Blockchain Workbench` in the **Search the Marketplace** search bar.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-218">Search for `Azure Blockchain Workbench` in the **Search the Marketplace** search bar.</span></span> 

    ![Marketplace search bar](media/blockchain-workbench-deploy/marketplace-search-bar.png)

4.  <span data-ttu-id="3b7b1-220">Select **Azure Blockchain Workbench**.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-220">Select **Azure Blockchain Workbench**.</span></span>

    ![Marketplace search results](media/blockchain-workbench-deploy/marketplace-search-results.png)

4.  <span data-ttu-id="3b7b1-222">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-222">Select **Create**.</span></span>
5.  <span data-ttu-id="3b7b1-223">Complete the basic settings.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-223">Complete the basic settings.</span></span>

    ![Create Azure Blockchain Workbench](media/blockchain-workbench-deploy/blockchain-workbench-settings-basic.png)

    | <span data-ttu-id="3b7b1-225">Setting</span><span class="sxs-lookup"><span data-stu-id="3b7b1-225">Setting</span></span> | <span data-ttu-id="3b7b1-226">Description</span><span class="sxs-lookup"><span data-stu-id="3b7b1-226">Description</span></span>  |
    |---------|--------------|
    | <span data-ttu-id="3b7b1-227">Resource prefix</span><span class="sxs-lookup"><span data-stu-id="3b7b1-227">Resource prefix</span></span> | <span data-ttu-id="3b7b1-228">Short unique identifier for your deployment.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-228">Short unique identifier for your deployment.</span></span> <span data-ttu-id="3b7b1-229">This value is used as a base for naming resources.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-229">This value is used as a base for naming resources.</span></span> |
    | <span data-ttu-id="3b7b1-230">VM user name</span><span class="sxs-lookup"><span data-stu-id="3b7b1-230">VM user name</span></span> | <span data-ttu-id="3b7b1-231">The user name is used as administrator for all virtual machines (VM).</span><span class="sxs-lookup"><span data-stu-id="3b7b1-231">The user name is used as administrator for all virtual machines (VM).</span></span> |
    | <span data-ttu-id="3b7b1-232">Authentication type</span><span class="sxs-lookup"><span data-stu-id="3b7b1-232">Authentication type</span></span> | <span data-ttu-id="3b7b1-233">Select if you want to use a password or key for connecting to VMs.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-233">Select if you want to use a password or key for connecting to VMs.</span></span> |
    | <span data-ttu-id="3b7b1-234">Password</span><span class="sxs-lookup"><span data-stu-id="3b7b1-234">Password</span></span> | <span data-ttu-id="3b7b1-235">The password is used for connecting to VMs.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-235">The password is used for connecting to VMs.</span></span> |
    | <span data-ttu-id="3b7b1-236">SSH</span><span class="sxs-lookup"><span data-stu-id="3b7b1-236">SSH</span></span> | <span data-ttu-id="3b7b1-237">Use an RSA public key in the single-line format beginning  with **ssh-rsa** or use the multi-line PEM format.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-237">Use an RSA public key in the single-line format beginning  with **ssh-rsa** or use the multi-line PEM format.</span></span> <span data-ttu-id="3b7b1-238">You can generate SSH keys using `ssh-keygen` on Linux and OS X, or by using PuTTYGen on Windows.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-238">You can generate SSH keys using `ssh-keygen` on Linux and OS X, or by using PuTTYGen on Windows.</span></span> <span data-ttu-id="3b7b1-239">More information on SSH keys, see [How to use SSH keys with Windows on Azure](../virtual-machines/linux/ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="3b7b1-239">More information on SSH keys, see [How to use SSH keys with Windows on Azure](../virtual-machines/linux/ssh-from-windows.md).</span></span> |
    | <span data-ttu-id="3b7b1-240">Database password / Confirm database password</span><span class="sxs-lookup"><span data-stu-id="3b7b1-240">Database password / Confirm database password</span></span> | <span data-ttu-id="3b7b1-241">Specify the password to use for access to the database created as part of the deployment.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-241">Specify the password to use for access to the database created as part of the deployment.</span></span> |
    | <span data-ttu-id="3b7b1-242">Deployment region</span><span class="sxs-lookup"><span data-stu-id="3b7b1-242">Deployment region</span></span> | <span data-ttu-id="3b7b1-243">Specify where to deploy Blockchain Workbench resources.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-243">Specify where to deploy Blockchain Workbench resources.</span></span> <span data-ttu-id="3b7b1-244">For best availability, this should match the **Location** setting.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-244">For best availability, this should match the **Location** setting.</span></span> |
    | <span data-ttu-id="3b7b1-245">Subscription</span><span class="sxs-lookup"><span data-stu-id="3b7b1-245">Subscription</span></span> | <span data-ttu-id="3b7b1-246">Specify the Azure Subscription you wish to use for your deployment.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-246">Specify the Azure Subscription you wish to use for your deployment.</span></span> |
    | <span data-ttu-id="3b7b1-247">Resource groups</span><span class="sxs-lookup"><span data-stu-id="3b7b1-247">Resource groups</span></span> | <span data-ttu-id="3b7b1-248">Create a new Resource group by selecting **Create new** and specify a unique resource group name.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-248">Create a new Resource group by selecting **Create new** and specify a unique resource group name.</span></span> |
    | <span data-ttu-id="3b7b1-249">Location</span><span class="sxs-lookup"><span data-stu-id="3b7b1-249">Location</span></span> | <span data-ttu-id="3b7b1-250">Specify the region you wish to deploy the framework.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-250">Specify the region you wish to deploy the framework.</span></span> |

6.  <span data-ttu-id="3b7b1-251">Select **OK** to finish the basic setting configuration section.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-251">Select **OK** to finish the basic setting configuration section.</span></span>

7.  <span data-ttu-id="3b7b1-252">Complete the **Azure Active Directory setup**.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-252">Complete the **Azure Active Directory setup**.</span></span>

    ![Azure AD Setup](media/blockchain-workbench-deploy/blockchain-workbench-settings-aad.png)

    | <span data-ttu-id="3b7b1-254">Setting</span><span class="sxs-lookup"><span data-stu-id="3b7b1-254">Setting</span></span> | <span data-ttu-id="3b7b1-255">Description</span><span class="sxs-lookup"><span data-stu-id="3b7b1-255">Description</span></span>  |
    |---------|--------------|
    | <span data-ttu-id="3b7b1-256">Domain Name</span><span class="sxs-lookup"><span data-stu-id="3b7b1-256">Domain Name</span></span> | <span data-ttu-id="3b7b1-257">Use the Azure AD tenant collected in the [Get tenant domain name](#get-tenant-domain-name) prerequisite section.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-257">Use the Azure AD tenant collected in the [Get tenant domain name](#get-tenant-domain-name) prerequisite section.</span></span> |
    | <span data-ttu-id="3b7b1-258">Application ID</span><span class="sxs-lookup"><span data-stu-id="3b7b1-258">Application ID</span></span> | <span data-ttu-id="3b7b1-259">Use the Application ID from the Blockchain client app registration collected in the [Get application ID](#get-application-id) prerequisite section.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-259">Use the Application ID from the Blockchain client app registration collected in the [Get application ID](#get-application-id) prerequisite section.</span></span> |
    | <span data-ttu-id="3b7b1-260">Application Key</span><span class="sxs-lookup"><span data-stu-id="3b7b1-260">Application Key</span></span> | <span data-ttu-id="3b7b1-261">Use the Application key from the Blockchain client app registration collected in the [Add Graph API key to application](#add-graph-api-key-to-application) prerequisite section.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-261">Use the Application key from the Blockchain client app registration collected in the [Add Graph API key to application](#add-graph-api-key-to-application) prerequisite section.</span></span> |


8.  <span data-ttu-id="3b7b1-262">Click **OK** to finish the Azure AD Parameters configuration section.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-262">Click **OK** to finish the Azure AD Parameters configuration section.</span></span>

9.  <span data-ttu-id="3b7b1-263">In **Network Settings and Performance**, choose if you want to create a new blockchain network or use an existing proof-of-authority blockchain network.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-263">In **Network Settings and Performance**, choose if you want to create a new blockchain network or use an existing proof-of-authority blockchain network.</span></span>

    <span data-ttu-id="3b7b1-264">For **Create new**:</span><span class="sxs-lookup"><span data-stu-id="3b7b1-264">For **Create new**:</span></span>

    <span data-ttu-id="3b7b1-265">The *create new* option creates a set of Ethereum Proof-of Authority (PoA) nodes within a single member’s subscription.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-265">The *create new* option creates a set of Ethereum Proof-of Authority (PoA) nodes within a single member’s subscription.</span></span> 

    ![Network settings and performance](media/blockchain-workbench-deploy/blockchain-workbench-settings-network-new.png)

    | <span data-ttu-id="3b7b1-267">Setting</span><span class="sxs-lookup"><span data-stu-id="3b7b1-267">Setting</span></span> | <span data-ttu-id="3b7b1-268">Description</span><span class="sxs-lookup"><span data-stu-id="3b7b1-268">Description</span></span>  |
    |---------|--------------|
    | <span data-ttu-id="3b7b1-269">Number of blockchain nodes</span><span class="sxs-lookup"><span data-stu-id="3b7b1-269">Number of blockchain nodes</span></span> | <span data-ttu-id="3b7b1-270">Choose the number of Ethereum PoA validator nodes to be deployed in your network.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-270">Choose the number of Ethereum PoA validator nodes to be deployed in your network.</span></span> |
    | <span data-ttu-id="3b7b1-271">Storage performance</span><span class="sxs-lookup"><span data-stu-id="3b7b1-271">Storage performance</span></span> | <span data-ttu-id="3b7b1-272">Choose the preferred VM storage performance for your blockchain network.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-272">Choose the preferred VM storage performance for your blockchain network.</span></span> |
    | <span data-ttu-id="3b7b1-273">Virtual machine size</span><span class="sxs-lookup"><span data-stu-id="3b7b1-273">Virtual machine size</span></span> | <span data-ttu-id="3b7b1-274">Choose the preferred VM size for your blockchain network.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-274">Choose the preferred VM size for your blockchain network.</span></span> |

    <span data-ttu-id="3b7b1-275">For **Use existing**:</span><span class="sxs-lookup"><span data-stu-id="3b7b1-275">For **Use existing**:</span></span>

    <span data-ttu-id="3b7b1-276">The *use existing* option allows you to specify an Ethereum Proof-of-Authority (PoA) blockchain network.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-276">The *use existing* option allows you to specify an Ethereum Proof-of-Authority (PoA) blockchain network.</span></span> <span data-ttu-id="3b7b1-277">Endpoints have the following requirements.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-277">Endpoints have the following requirements.</span></span>

    * <span data-ttu-id="3b7b1-278">The endpoint must be an Ethereum Proof-of-Authority (PoA) blockchain network.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-278">The endpoint must be an Ethereum Proof-of-Authority (PoA) blockchain network.</span></span>
    * <span data-ttu-id="3b7b1-279">The endpoint must be publicly accessible over the network.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-279">The endpoint must be publicly accessible over the network.</span></span>
    * <span data-ttu-id="3b7b1-280">The PoA blockchain network should be configured to have gas price set to zero (Note: Blockchain Workbench accounts are not funded.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-280">The PoA blockchain network should be configured to have gas price set to zero (Note: Blockchain Workbench accounts are not funded.</span></span> <span data-ttu-id="3b7b1-281">If funds are required, the transactions fail).</span><span class="sxs-lookup"><span data-stu-id="3b7b1-281">If funds are required, the transactions fail).</span></span>

    ![Network settings and performance](media/blockchain-workbench-deploy/blockchain-workbench-settings-network-existing.png)

    | <span data-ttu-id="3b7b1-283">Setting</span><span class="sxs-lookup"><span data-stu-id="3b7b1-283">Setting</span></span> | <span data-ttu-id="3b7b1-284">Description</span><span class="sxs-lookup"><span data-stu-id="3b7b1-284">Description</span></span>  |
    |---------|--------------|
    | <span data-ttu-id="3b7b1-285">Ethereum RPC Endpoint</span><span class="sxs-lookup"><span data-stu-id="3b7b1-285">Ethereum RPC Endpoint</span></span> | <span data-ttu-id="3b7b1-286">Provide the RPC endpoint of an existing PoA blockchain network.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-286">Provide the RPC endpoint of an existing PoA blockchain network.</span></span> <span data-ttu-id="3b7b1-287">The endpoint starts with http:// and ends with a port number.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-287">The endpoint starts with http:// and ends with a port number.</span></span> <span data-ttu-id="3b7b1-288">For example, `http://contoso-chain.onmicrosoft.com:8545`</span><span class="sxs-lookup"><span data-stu-id="3b7b1-288">For example, `http://contoso-chain.onmicrosoft.com:8545`</span></span> |
    | <span data-ttu-id="3b7b1-289">Storage performance</span><span class="sxs-lookup"><span data-stu-id="3b7b1-289">Storage performance</span></span> | <span data-ttu-id="3b7b1-290">Choose the preferred VM storage performance for your blockchain network.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-290">Choose the preferred VM storage performance for your blockchain network.</span></span> |
    | <span data-ttu-id="3b7b1-291">Virtual machine size</span><span class="sxs-lookup"><span data-stu-id="3b7b1-291">Virtual machine size</span></span> | <span data-ttu-id="3b7b1-292">Choose the preferred VM size for your blockchain network.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-292">Choose the preferred VM size for your blockchain network.</span></span> |

10. <span data-ttu-id="3b7b1-293">Select **OK** to finish network settings and performance.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-293">Select **OK** to finish network settings and performance.</span></span>

11. <span data-ttu-id="3b7b1-294">Complete the **Azure Monitor** settings.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-294">Complete the **Azure Monitor** settings.</span></span>

    ![Azure Monitor](media/blockchain-workbench-deploy/blockchain-workbench-settings-oms.png)

    | <span data-ttu-id="3b7b1-296">Setting</span><span class="sxs-lookup"><span data-stu-id="3b7b1-296">Setting</span></span> | <span data-ttu-id="3b7b1-297">Description</span><span class="sxs-lookup"><span data-stu-id="3b7b1-297">Description</span></span>  |
    |---------|--------------|
    | <span data-ttu-id="3b7b1-298">Monitoring</span><span class="sxs-lookup"><span data-stu-id="3b7b1-298">Monitoring</span></span> | <span data-ttu-id="3b7b1-299">Choose whether you want to enable Azure Monitor to monitor your blockchain network</span><span class="sxs-lookup"><span data-stu-id="3b7b1-299">Choose whether you want to enable Azure Monitor to monitor your blockchain network</span></span> |
    | <span data-ttu-id="3b7b1-300">Connect to existing Log Analytics instance</span><span class="sxs-lookup"><span data-stu-id="3b7b1-300">Connect to existing Log Analytics instance</span></span> | <span data-ttu-id="3b7b1-301">Choose whether you want to use an existing Log Analytics instance or create a new one.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-301">Choose whether you want to use an existing Log Analytics instance or create a new one.</span></span> <span data-ttu-id="3b7b1-302">If using an existing instance, enter your workspace ID and primary key.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-302">If using an existing instance, enter your workspace ID and primary key.</span></span> |

12. <span data-ttu-id="3b7b1-303">Click **OK** to finish the Azure Monitor section.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-303">Click **OK** to finish the Azure Monitor section.</span></span>

13. <span data-ttu-id="3b7b1-304">Review the summary to verify your parameters are accurate.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-304">Review the summary to verify your parameters are accurate.</span></span>

    ![Summary](media/blockchain-workbench-deploy/blockchain-workbench-summary.png)

14. <span data-ttu-id="3b7b1-306">Select **Create** to agree to the terms and deploy your Azure Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-306">Select **Create** to agree to the terms and deploy your Azure Blockchain Workbench.</span></span>

<span data-ttu-id="3b7b1-307">The deployment can take up to 90 minutes.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-307">The deployment can take up to 90 minutes.</span></span> <span data-ttu-id="3b7b1-308">You can use the Azure portal to monitor progress.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-308">You can use the Azure portal to monitor progress.</span></span> <span data-ttu-id="3b7b1-309">In the newly created resource group, select **Deployments > Overview** to see the status of the deployed artifacts.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-309">In the newly created resource group, select **Deployments > Overview** to see the status of the deployed artifacts.</span></span>

## <a name="blockchain-workbench-web-url"></a><span data-ttu-id="3b7b1-310">Blockchain Workbench Web URL</span><span class="sxs-lookup"><span data-stu-id="3b7b1-310">Blockchain Workbench Web URL</span></span>

<span data-ttu-id="3b7b1-311">Once the deployment of the Blockchain Workbench has completed, a new resource group contains your Blockchain Workbench resources.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-311">Once the deployment of the Blockchain Workbench has completed, a new resource group contains your Blockchain Workbench resources.</span></span> <span data-ttu-id="3b7b1-312">Blockchain Workbench services are accessed through a web URL.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-312">Blockchain Workbench services are accessed through a web URL.</span></span> <span data-ttu-id="3b7b1-313">The following steps show you how to retrieve the web URL of the deployed framework.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-313">The following steps show you how to retrieve the web URL of the deployed framework.</span></span>

1. <span data-ttu-id="3b7b1-314">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3b7b1-314">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3b7b1-315">In the left-hand navigation pane, select **Resource groups**</span><span class="sxs-lookup"><span data-stu-id="3b7b1-315">In the left-hand navigation pane, select **Resource groups**</span></span>
3. <span data-ttu-id="3b7b1-316">Choose the resource group name you specified when deploying Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-316">Choose the resource group name you specified when deploying Blockchain Workbench.</span></span>
4. <span data-ttu-id="3b7b1-317">Click the **TYPE** column heading to sort the list alphabetically by type.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-317">Click the **TYPE** column heading to sort the list alphabetically by type.</span></span>
5. <span data-ttu-id="3b7b1-318">There are two resources with type **App Service**.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-318">There are two resources with type **App Service**.</span></span> <span data-ttu-id="3b7b1-319">Select the resource of type **App Service** *without* the "-api" suffix.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-319">Select the resource of type **App Service** *without* the "-api" suffix.</span></span>

    ![App service list](media/blockchain-workbench-deploy/resource-group-list.png)

6.  <span data-ttu-id="3b7b1-321">In the App Service **Essentials** section, copy the **URL** value, which represents the web URL to your deployed Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-321">In the App Service **Essentials** section, copy the **URL** value, which represents the web URL to your deployed Blockchain Workbench.</span></span>

    ![App service essentials](media/blockchain-workbench-deploy/app-service.png)

<span data-ttu-id="3b7b1-323">To associate a custom domain name with Blockchain Workbench, see [configuring a custom domain name for a web app in Azure App Service using Traffic Manager](../app-service/web-sites-traffic-manager-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="3b7b1-323">To associate a custom domain name with Blockchain Workbench, see [configuring a custom domain name for a web app in Azure App Service using Traffic Manager](../app-service/web-sites-traffic-manager-custom-domain-name.md).</span></span>

## <a name="configuring-the-reply-url"></a><span data-ttu-id="3b7b1-324">Configuring the Reply URL</span><span class="sxs-lookup"><span data-stu-id="3b7b1-324">Configuring the Reply URL</span></span>

<span data-ttu-id="3b7b1-325">Once the Azure Blockchain Workbench has been deployed, the next step is to make sure the Azure Active Directory (Azure AD) client application is registered to the correct **Reply URL** of the deployed Blockchain Workbench web URL.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-325">Once the Azure Blockchain Workbench has been deployed, the next step is to make sure the Azure Active Directory (Azure AD) client application is registered to the correct **Reply URL** of the deployed Blockchain Workbench web URL.</span></span>

1. <span data-ttu-id="3b7b1-326">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3b7b1-326">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3b7b1-327">Verify you are in the tenant where you registered the Azure AD client application.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-327">Verify you are in the tenant where you registered the Azure AD client application.</span></span>
3. <span data-ttu-id="3b7b1-328">In the left-hand navigation pane, select the **Azure Active Directory** service.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-328">In the left-hand navigation pane, select the **Azure Active Directory** service.</span></span> <span data-ttu-id="3b7b1-329">Select **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-329">Select **App registrations**.</span></span>
4. <span data-ttu-id="3b7b1-330">Select the Azure AD client application you registered in the prerequisite section.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-330">Select the Azure AD client application you registered in the prerequisite section.</span></span>
5. <span data-ttu-id="3b7b1-331">Select **Settings > Reply URLs**.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-331">Select **Settings > Reply URLs**.</span></span>
6. <span data-ttu-id="3b7b1-332">Specify the main web URL of the Azure Blockchain Workbench deployment you retrieved in the **Get the Azure Blockchain Workbench Web URL** section.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-332">Specify the main web URL of the Azure Blockchain Workbench deployment you retrieved in the **Get the Azure Blockchain Workbench Web URL** section.</span></span> <span data-ttu-id="3b7b1-333">The Reply URL is prefixed with `https://`.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-333">The Reply URL is prefixed with `https://`.</span></span> <span data-ttu-id="3b7b1-334">For example, `https://myblockchain2-7v75.azurewebsites.net`</span><span class="sxs-lookup"><span data-stu-id="3b7b1-334">For example, `https://myblockchain2-7v75.azurewebsites.net`</span></span>

    ![Reply URLs](media/blockchain-workbench-deploy/configure-reply-url.png)

7. <span data-ttu-id="3b7b1-336">Select **Save** to update the client registration.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-336">Select **Save** to update the client registration.</span></span>

## <a name="remove-a-deployment"></a><span data-ttu-id="3b7b1-337">Remove a deployment</span><span class="sxs-lookup"><span data-stu-id="3b7b1-337">Remove a deployment</span></span>

<span data-ttu-id="3b7b1-338">When a deployment is no longer needed, you can remove a deployment by deleting the Blockchain Workbench resource group.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-338">When a deployment is no longer needed, you can remove a deployment by deleting the Blockchain Workbench resource group.</span></span>

1. <span data-ttu-id="3b7b1-339">In the Azure portal, navigate to **Resource group** in the left navigation pane and select the resource group you want to delete.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-339">In the Azure portal, navigate to **Resource group** in the left navigation pane and select the resource group you want to delete.</span></span> 
2. <span data-ttu-id="3b7b1-340">Select **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-340">Select **Delete resource group**.</span></span> <span data-ttu-id="3b7b1-341">Verify deletion by entering the resource group name and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-341">Verify deletion by entering the resource group name and select **Delete**.</span></span>

    ![Delete resource group](media/blockchain-workbench-deploy/delete-resource-group.png)

## <a name="next-steps"></a><span data-ttu-id="3b7b1-343">Next steps</span><span class="sxs-lookup"><span data-stu-id="3b7b1-343">Next steps</span></span>

<span data-ttu-id="3b7b1-344">In this how-to article, you deployed Azure Blockchain Workbench.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-344">In this how-to article, you deployed Azure Blockchain Workbench.</span></span> <span data-ttu-id="3b7b1-345">To learn how to create a blockchain application, continue to the next how-to article.</span><span class="sxs-lookup"><span data-stu-id="3b7b1-345">To learn how to create a blockchain application, continue to the next how-to article.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3b7b1-346">Create a blockchain application in Azure Blockchain Workbench</span><span class="sxs-lookup"><span data-stu-id="3b7b1-346">Create a blockchain application in Azure Blockchain Workbench</span></span>](blockchain-workbench-create-app.md)
