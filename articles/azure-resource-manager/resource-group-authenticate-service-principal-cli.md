---
title: Create identity for Azure app with Azure CLI | Microsoft Docs
description: Describes how to use Azure CLI to create an Active Directory application and service principal, and grant it access to resources through role-based access control. It shows how to authenticate application with a password or certificate.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: 4ea75e08a630ad777444ea3a3cb85f4bb0efe01f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564363"
---
# <a name="use-azure-cli-to-create-a-service-principal-to-access-resources"></a><span data-ttu-id="70f6a-104">Use Azure CLI to create a service principal to access resources</span><span class="sxs-lookup"><span data-stu-id="70f6a-104">Use Azure CLI to create a service principal to access resources</span></span>
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-authenticate-service-principal.md)
> * [Azure CLI](resource-group-authenticate-service-principal-cli.md)
> * [Portal](resource-group-create-service-principal-portal.md)
> 
> 

<span data-ttu-id="70f6a-108">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span><span class="sxs-lookup"><span data-stu-id="70f6a-108">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span></span> <span data-ttu-id="70f6a-109">This identity is known as a service principal.</span><span class="sxs-lookup"><span data-stu-id="70f6a-109">This identity is known as a service principal.</span></span> <span data-ttu-id="70f6a-110">This approach enables you to:</span><span class="sxs-lookup"><span data-stu-id="70f6a-110">This approach enables you to:</span></span>

* <span data-ttu-id="70f6a-111">Assign permissions to the app identity that are different than your own permissions.</span><span class="sxs-lookup"><span data-stu-id="70f6a-111">Assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="70f6a-112">Typically, these permissions are restricted to exactly what the app needs to do.</span><span class="sxs-lookup"><span data-stu-id="70f6a-112">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="70f6a-113">Use a certificate for authentication when executing an unattended script.</span><span class="sxs-lookup"><span data-stu-id="70f6a-113">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="70f6a-114">This article shows you how to use [Azure CLI 1.0](../cli-install-nodejs.md) to set up an application to run under its own credentials and identity.</span><span class="sxs-lookup"><span data-stu-id="70f6a-114">This article shows you how to use [Azure CLI 1.0](../cli-install-nodejs.md) to set up an application to run under its own credentials and identity.</span></span> <span data-ttu-id="70f6a-115">Install the latest version of [Azure CLI 1.0](../cli-install-nodejs.md) to make sure your environment matches the examples in this article.</span><span class="sxs-lookup"><span data-stu-id="70f6a-115">Install the latest version of [Azure CLI 1.0](../cli-install-nodejs.md) to make sure your environment matches the examples in this article.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="70f6a-116">Required permissions</span><span class="sxs-lookup"><span data-stu-id="70f6a-116">Required permissions</span></span>
<span data-ttu-id="70f6a-117">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="70f6a-117">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="70f6a-118">Specifically, you must be able to create an app in the Active Directory, and assign the service principal to a role.</span><span class="sxs-lookup"><span data-stu-id="70f6a-118">Specifically, you must be able to create an app in the Active Directory, and assign the service principal to a role.</span></span> 

<span data-ttu-id="70f6a-119">The easiest way to check whether your account has adequate permissions is through the portal.</span><span class="sxs-lookup"><span data-stu-id="70f6a-119">The easiest way to check whether your account has adequate permissions is through the portal.</span></span> <span data-ttu-id="70f6a-120">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="70f6a-120">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="70f6a-121">Now, proceed to a section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span><span class="sxs-lookup"><span data-stu-id="70f6a-121">Now, proceed to a section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="70f6a-122">Create service principal with password</span><span class="sxs-lookup"><span data-stu-id="70f6a-122">Create service principal with password</span></span>
<span data-ttu-id="70f6a-123">In this section, you perform the steps to create the AD application with a password, and assign the Reader role to the service principal.</span><span class="sxs-lookup"><span data-stu-id="70f6a-123">In this section, you perform the steps to create the AD application with a password, and assign the Reader role to the service principal.</span></span>

1. <span data-ttu-id="70f6a-124">Sign in to your account.</span><span class="sxs-lookup"><span data-stu-id="70f6a-124">Sign in to your account.</span></span>
   
   ```azurecli
   azure login
   ```
2. <span data-ttu-id="70f6a-125">To create an app identity, provide the name of the app and a password, as shown in the following command:</span><span class="sxs-lookup"><span data-stu-id="70f6a-125">To create an app identity, provide the name of the app and a password, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   <span data-ttu-id="70f6a-126">The new service principal is returned.</span><span class="sxs-lookup"><span data-stu-id="70f6a-126">The new service principal is returned.</span></span> <span data-ttu-id="70f6a-127">The Object Id is needed when granting permissions.</span><span class="sxs-lookup"><span data-stu-id="70f6a-127">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="70f6a-128">The guid listed with the Service Principal Names is needed when logging in.</span><span class="sxs-lookup"><span data-stu-id="70f6a-128">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="70f6a-129">This guid is the same value as the app id. In the sample applications, this value is referred to as the `Client ID`.</span><span class="sxs-lookup"><span data-stu-id="70f6a-129">This guid is the same value as the app id. In the sample applications, this value is referred to as the `Client ID`.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. <span data-ttu-id="70f6a-130">Grant the service principal permissions on your subscription.</span><span class="sxs-lookup"><span data-stu-id="70f6a-130">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="70f6a-131">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span><span class="sxs-lookup"><span data-stu-id="70f6a-131">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="70f6a-132">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="70f6a-132">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="70f6a-133">For the objectid parameter, provide the Object Id that you used when creating the application.</span><span class="sxs-lookup"><span data-stu-id="70f6a-133">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="70f6a-134">Before running this command, you must allow some time for the new service principal to propagate throughout Active Directory.</span><span class="sxs-lookup"><span data-stu-id="70f6a-134">Before running this command, you must allow some time for the new service principal to propagate throughout Active Directory.</span></span> <span data-ttu-id="70f6a-135">When you run these commands manually, usually enough time has elapsed between tasks.</span><span class="sxs-lookup"><span data-stu-id="70f6a-135">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="70f6a-136">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="70f6a-136">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="70f6a-137">If you see an error stating the principal does not exist in the directory, rerun the command.</span><span class="sxs-lookup"><span data-stu-id="70f6a-137">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
<span data-ttu-id="70f6a-138">That's it!</span><span class="sxs-lookup"><span data-stu-id="70f6a-138">That's it!</span></span> <span data-ttu-id="70f6a-139">Your AD application and service principal are set up.</span><span class="sxs-lookup"><span data-stu-id="70f6a-139">Your AD application and service principal are set up.</span></span> <span data-ttu-id="70f6a-140">The next section shows you how to log in with the credential through Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="70f6a-140">The next section shows you how to log in with the credential through Azure CLI.</span></span> <span data-ttu-id="70f6a-141">If you want to use the credential in your code application, you do not need to continue with this topic.</span><span class="sxs-lookup"><span data-stu-id="70f6a-141">If you want to use the credential in your code application, you do not need to continue with this topic.</span></span> <span data-ttu-id="70f6a-142">You can jump to the [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span><span class="sxs-lookup"><span data-stu-id="70f6a-142">You can jump to the [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span></span> 

### <a name="provide-credentials-through-azure-cli"></a><span data-ttu-id="70f6a-143">Provide credentials through Azure CLI</span><span class="sxs-lookup"><span data-stu-id="70f6a-143">Provide credentials through Azure CLI</span></span>
<span data-ttu-id="70f6a-144">Now, you need to log in as the application to perform operations.</span><span class="sxs-lookup"><span data-stu-id="70f6a-144">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="70f6a-145">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span><span class="sxs-lookup"><span data-stu-id="70f6a-145">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="70f6a-146">A tenant is an instance of Active Directory.</span><span class="sxs-lookup"><span data-stu-id="70f6a-146">A tenant is an instance of Active Directory.</span></span> <span data-ttu-id="70f6a-147">To retrieve the tenant id for your currently authenticated subscription, use:</span><span class="sxs-lookup"><span data-stu-id="70f6a-147">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="70f6a-148">Which returns:</span><span class="sxs-lookup"><span data-stu-id="70f6a-148">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     <span data-ttu-id="70f6a-149">If you need to get the tenant id of another subscription, use the following command:</span><span class="sxs-lookup"><span data-stu-id="70f6a-149">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="70f6a-150">If you need to retrieve the client id to use for logging in, use:</span><span class="sxs-lookup"><span data-stu-id="70f6a-150">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     <span data-ttu-id="70f6a-151">The value to use for logging in is the guid listed in the service principal names.</span><span class="sxs-lookup"><span data-stu-id="70f6a-151">The value to use for logging in is the guid listed in the service principal names.</span></span>
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. <span data-ttu-id="70f6a-152">Log in as the service principal.</span><span class="sxs-lookup"><span data-stu-id="70f6a-152">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    <span data-ttu-id="70f6a-153">You are prompted for the password.</span><span class="sxs-lookup"><span data-stu-id="70f6a-153">You are prompted for the password.</span></span> <span data-ttu-id="70f6a-154">Provide the password you specified when creating the AD application.</span><span class="sxs-lookup"><span data-stu-id="70f6a-154">Provide the password you specified when creating the AD application.</span></span>
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

<span data-ttu-id="70f6a-155">You are now authenticated as the service principal for the service principal that you created.</span><span class="sxs-lookup"><span data-stu-id="70f6a-155">You are now authenticated as the service principal for the service principal that you created.</span></span>

<span data-ttu-id="70f6a-156">Alternatively, you can invoke REST operations from the command line to log in.</span><span class="sxs-lookup"><span data-stu-id="70f6a-156">Alternatively, you can invoke REST operations from the command line to log in.</span></span> <span data-ttu-id="70f6a-157">From the authentication response, you can retrieve the access token for use with other operations.</span><span class="sxs-lookup"><span data-stu-id="70f6a-157">From the authentication response, you can retrieve the access token for use with other operations.</span></span> <span data-ttu-id="70f6a-158">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="70f6a-158">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="create-service-principal-with-certificate"></a><span data-ttu-id="70f6a-159">Create service principal with certificate</span><span class="sxs-lookup"><span data-stu-id="70f6a-159">Create service principal with certificate</span></span>
<span data-ttu-id="70f6a-160">In this section, you perform the steps to:</span><span class="sxs-lookup"><span data-stu-id="70f6a-160">In this section, you perform the steps to:</span></span>

* <span data-ttu-id="70f6a-161">create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="70f6a-161">create a self-signed certificate</span></span>
* <span data-ttu-id="70f6a-162">create the AD application with the certificate, and the service principal</span><span class="sxs-lookup"><span data-stu-id="70f6a-162">create the AD application with the certificate, and the service principal</span></span>
* <span data-ttu-id="70f6a-163">assign the Reader role to the service principal</span><span class="sxs-lookup"><span data-stu-id="70f6a-163">assign the Reader role to the service principal</span></span>

<span data-ttu-id="70f6a-164">To complete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span><span class="sxs-lookup"><span data-stu-id="70f6a-164">To complete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span></span>

1. <span data-ttu-id="70f6a-165">Create a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="70f6a-165">Create a self-signed certificate.</span></span>
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. <span data-ttu-id="70f6a-166">The preceding step created two files - privkey.pem and cert.pem.</span><span class="sxs-lookup"><span data-stu-id="70f6a-166">The preceding step created two files - privkey.pem and cert.pem.</span></span> <span data-ttu-id="70f6a-167">Combine the public and private keys into a single file.</span><span class="sxs-lookup"><span data-stu-id="70f6a-167">Combine the public and private keys into a single file.</span></span>

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. <span data-ttu-id="70f6a-168">Open the **examplecert.pem** file and look for the long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span><span class="sxs-lookup"><span data-stu-id="70f6a-168">Open the **examplecert.pem** file and look for the long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span></span> <span data-ttu-id="70f6a-169">Copy the certificate data.</span><span class="sxs-lookup"><span data-stu-id="70f6a-169">Copy the certificate data.</span></span> <span data-ttu-id="70f6a-170">You pass this data as a parameter when creating the service principal.</span><span class="sxs-lookup"><span data-stu-id="70f6a-170">You pass this data as a parameter when creating the service principal.</span></span>

4. <span data-ttu-id="70f6a-171">Sign in to your account.</span><span class="sxs-lookup"><span data-stu-id="70f6a-171">Sign in to your account.</span></span>

   ```azurecli
   azure login
   ```
5. <span data-ttu-id="70f6a-172">To create the service principal, provide the name of the app and the certificate data, as shown in the following command:</span><span class="sxs-lookup"><span data-stu-id="70f6a-172">To create the service principal, provide the name of the app and the certificate data, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   <span data-ttu-id="70f6a-173">The new service principal is returned.</span><span class="sxs-lookup"><span data-stu-id="70f6a-173">The new service principal is returned.</span></span> <span data-ttu-id="70f6a-174">The Object Id is needed when granting permissions.</span><span class="sxs-lookup"><span data-stu-id="70f6a-174">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="70f6a-175">The guid listed with the Service Principal Names is needed when logging in.</span><span class="sxs-lookup"><span data-stu-id="70f6a-175">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="70f6a-176">This guid is the same value as the app id. In the sample applications, this value is referred to as the Client ID.</span><span class="sxs-lookup"><span data-stu-id="70f6a-176">This guid is the same value as the app id. In the sample applications, this value is referred to as the Client ID.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. <span data-ttu-id="70f6a-177">Grant the service principal permissions on your subscription.</span><span class="sxs-lookup"><span data-stu-id="70f6a-177">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="70f6a-178">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span><span class="sxs-lookup"><span data-stu-id="70f6a-178">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="70f6a-179">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="70f6a-179">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="70f6a-180">For the objectid parameter, provide the Object Id that you used when creating the application.</span><span class="sxs-lookup"><span data-stu-id="70f6a-180">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="70f6a-181">Before running this command, you must allow some time for the new service principal to propagate throughout Active Directory.</span><span class="sxs-lookup"><span data-stu-id="70f6a-181">Before running this command, you must allow some time for the new service principal to propagate throughout Active Directory.</span></span> <span data-ttu-id="70f6a-182">When you run these commands manually, usually enough time has elapsed between tasks.</span><span class="sxs-lookup"><span data-stu-id="70f6a-182">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="70f6a-183">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="70f6a-183">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="70f6a-184">If you see an error stating the principal does not exist in the directory, rerun the command.</span><span class="sxs-lookup"><span data-stu-id="70f6a-184">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a><span data-ttu-id="70f6a-185">Provide certificate through automated Azure CLI script</span><span class="sxs-lookup"><span data-stu-id="70f6a-185">Provide certificate through automated Azure CLI script</span></span>
<span data-ttu-id="70f6a-186">Now, you need to log in as the application to perform operations.</span><span class="sxs-lookup"><span data-stu-id="70f6a-186">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="70f6a-187">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span><span class="sxs-lookup"><span data-stu-id="70f6a-187">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="70f6a-188">A tenant is an instance of Active Directory.</span><span class="sxs-lookup"><span data-stu-id="70f6a-188">A tenant is an instance of Active Directory.</span></span> <span data-ttu-id="70f6a-189">To retrieve the tenant id for your currently authenticated subscription, use:</span><span class="sxs-lookup"><span data-stu-id="70f6a-189">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="70f6a-190">Which returns:</span><span class="sxs-lookup"><span data-stu-id="70f6a-190">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   <span data-ttu-id="70f6a-191">If you need to get the tenant id of another subscription, use the following command:</span><span class="sxs-lookup"><span data-stu-id="70f6a-191">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="70f6a-192">To retrieve the certificate thumbprint and remove unneeded characters, use:</span><span class="sxs-lookup"><span data-stu-id="70f6a-192">To retrieve the certificate thumbprint and remove unneeded characters, use:</span></span>
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   <span data-ttu-id="70f6a-193">Which returns a thumbprint value similar to:</span><span class="sxs-lookup"><span data-stu-id="70f6a-193">Which returns a thumbprint value similar to:</span></span>
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. <span data-ttu-id="70f6a-194">If you need to retrieve the client id to use for logging in, use:</span><span class="sxs-lookup"><span data-stu-id="70f6a-194">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   <span data-ttu-id="70f6a-195">The value to use for logging in is the guid listed in the service principal names.</span><span class="sxs-lookup"><span data-stu-id="70f6a-195">The value to use for logging in is the guid listed in the service principal names.</span></span>
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. <span data-ttu-id="70f6a-196">Log in as the service principal.</span><span class="sxs-lookup"><span data-stu-id="70f6a-196">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

<span data-ttu-id="70f6a-197">You are now authenticated as the service principal for the Active Directory application that you created.</span><span class="sxs-lookup"><span data-stu-id="70f6a-197">You are now authenticated as the service principal for the Active Directory application that you created.</span></span>

## <a name="change-credentials"></a><span data-ttu-id="70f6a-198">Change credentials</span><span class="sxs-lookup"><span data-stu-id="70f6a-198">Change credentials</span></span>

<span data-ttu-id="70f6a-199">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span><span class="sxs-lookup"><span data-stu-id="70f6a-199">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span></span>

<span data-ttu-id="70f6a-200">To change a password, use:</span><span class="sxs-lookup"><span data-stu-id="70f6a-200">To change a password, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

<span data-ttu-id="70f6a-201">To change a certificate value, use:</span><span class="sxs-lookup"><span data-stu-id="70f6a-201">To change a certificate value, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a><span data-ttu-id="70f6a-202">Debug</span><span class="sxs-lookup"><span data-stu-id="70f6a-202">Debug</span></span>

<span data-ttu-id="70f6a-203">You may encounter the following errors when creating a service principal:</span><span class="sxs-lookup"><span data-stu-id="70f6a-203">You may encounter the following errors when creating a service principal:</span></span>

* <span data-ttu-id="70f6a-204">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span><span class="sxs-lookup"><span data-stu-id="70f6a-204">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span></span> <span data-ttu-id="70f6a-205">- You see this error when your account does not have the [required permissions](#required-permissions) on the Active Directory to register an app.</span><span class="sxs-lookup"><span data-stu-id="70f6a-205">- You see this error when your account does not have the [required permissions](#required-permissions) on the Active Directory to register an app.</span></span> <span data-ttu-id="70f6a-206">Typically, you see this error when only admin users in your Active Directory can register apps, and your account is not an admin. Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span><span class="sxs-lookup"><span data-stu-id="70f6a-206">Typically, you see this error when only admin users in your Active Directory can register apps, and your account is not an admin. Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

* <span data-ttu-id="70f6a-207">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span><span class="sxs-lookup"><span data-stu-id="70f6a-207">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span></span> <span data-ttu-id="70f6a-208">Ask your subscription administrator to add you to User Access Administrator role.</span><span class="sxs-lookup"><span data-stu-id="70f6a-208">Ask your subscription administrator to add you to User Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="70f6a-209">Sample applications</span><span class="sxs-lookup"><span data-stu-id="70f6a-209">Sample applications</span></span>
<span data-ttu-id="70f6a-210">The following sample applications show how to log in as the service principal.</span><span class="sxs-lookup"><span data-stu-id="70f6a-210">The following sample applications show how to log in as the service principal.</span></span>

<span data-ttu-id="70f6a-211">**.NET**</span><span class="sxs-lookup"><span data-stu-id="70f6a-211">**.NET**</span></span>

* [<span data-ttu-id="70f6a-212">Deploy an SSH Enabled VM with a Template with .NET</span><span class="sxs-lookup"><span data-stu-id="70f6a-212">Deploy an SSH Enabled VM with a Template with .NET</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-dotnet-template-deployment/)
* [<span data-ttu-id="70f6a-213">Manage Azure resources and resource groups with .NET</span><span class="sxs-lookup"><span data-stu-id="70f6a-213">Manage Azure resources and resource groups with .NET</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-dotnet-resources-and-groups/)

<span data-ttu-id="70f6a-214">**Java**</span><span class="sxs-lookup"><span data-stu-id="70f6a-214">**Java**</span></span>

* [<span data-ttu-id="70f6a-215">Getting Started with Resources - Deploy Using Azure Resource Manager Template - in Java</span><span class="sxs-lookup"><span data-stu-id="70f6a-215">Getting Started with Resources - Deploy Using Azure Resource Manager Template - in Java</span></span>](https://azure.microsoft.com/documentation/samples/resources-java-deploy-using-arm-template/)
* [<span data-ttu-id="70f6a-216">Getting Started with Resources - Manage Resource Group - in Java</span><span class="sxs-lookup"><span data-stu-id="70f6a-216">Getting Started with Resources - Manage Resource Group - in Java</span></span>](https://azure.microsoft.com/documentation/samples/resources-java-manage-resource-group//)

<span data-ttu-id="70f6a-217">**Python**</span><span class="sxs-lookup"><span data-stu-id="70f6a-217">**Python**</span></span>

* [<span data-ttu-id="70f6a-218">Deploy an SSH Enabled VM with a Template in Python</span><span class="sxs-lookup"><span data-stu-id="70f6a-218">Deploy an SSH Enabled VM with a Template in Python</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-python-template-deployment/)
* [<span data-ttu-id="70f6a-219">Managing Azure Resource and Resource Groups with Python</span><span class="sxs-lookup"><span data-stu-id="70f6a-219">Managing Azure Resource and Resource Groups with Python</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-python-resources-and-groups/)

<span data-ttu-id="70f6a-220">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="70f6a-220">**Node.js**</span></span>

* [<span data-ttu-id="70f6a-221">Deploy an SSH Enabled VM with a Template in Node.js</span><span class="sxs-lookup"><span data-stu-id="70f6a-221">Deploy an SSH Enabled VM with a Template in Node.js</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-node-template-deployment/)
* [<span data-ttu-id="70f6a-222">Manage Azure resources and resource groups with Node.js</span><span class="sxs-lookup"><span data-stu-id="70f6a-222">Manage Azure resources and resource groups with Node.js</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-node-resources-and-groups/)

<span data-ttu-id="70f6a-223">**Ruby**</span><span class="sxs-lookup"><span data-stu-id="70f6a-223">**Ruby**</span></span>

* [<span data-ttu-id="70f6a-224">Deploy an SSH Enabled VM with a Template in Ruby</span><span class="sxs-lookup"><span data-stu-id="70f6a-224">Deploy an SSH Enabled VM with a Template in Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-template-deployment/)
* [<span data-ttu-id="70f6a-225">Managing Azure Resource and Resource Groups with Ruby</span><span class="sxs-lookup"><span data-stu-id="70f6a-225">Managing Azure Resource and Resource Groups with Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="70f6a-226">Next Steps</span><span class="sxs-lookup"><span data-stu-id="70f6a-226">Next Steps</span></span>
* <span data-ttu-id="70f6a-227">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="70f6a-227">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="70f6a-228">To get more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="70f6a-228">To get more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span></span> 

