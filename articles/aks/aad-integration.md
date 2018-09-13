---
title: Integrate Azure Active Directory with Azure Kubernetes Service
description: How to create Azure Active Directory-enabled Azure Kubernetes Service (AKS) clusters.
services: container-service
author: iainfoulds
ms.service: container-service
ms.topic: article
ms.date: 8/9/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 5a93cb7b2abbf0eaa25304f61a8a422edf209959
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865189"
---
# <a name="integrate-azure-active-directory-with-aks"></a><span data-ttu-id="1e20f-103">Integrate Azure Active Directory with AKS</span><span class="sxs-lookup"><span data-stu-id="1e20f-103">Integrate Azure Active Directory with AKS</span></span>

<span data-ttu-id="1e20f-104">Azure Kubernetes Service (AKS) can be configured to use Azure Active Directory (AD) for user authentication.</span><span class="sxs-lookup"><span data-stu-id="1e20f-104">Azure Kubernetes Service (AKS) can be configured to use Azure Active Directory (AD) for user authentication.</span></span> <span data-ttu-id="1e20f-105">In this configuration, you can log into an AKS cluster using your Azure Active Directory authentication token.</span><span class="sxs-lookup"><span data-stu-id="1e20f-105">In this configuration, you can log into an AKS cluster using your Azure Active Directory authentication token.</span></span> <span data-ttu-id="1e20f-106">Additionally, cluster administrators are able to configure Kubernetes role-based access control (RBAC) based on a users identity or directory group membership.</span><span class="sxs-lookup"><span data-stu-id="1e20f-106">Additionally, cluster administrators are able to configure Kubernetes role-based access control (RBAC) based on a users identity or directory group membership.</span></span>

<span data-ttu-id="1e20f-107">This article shows you how to deploy the prerequisites for AKS and Azure AD, then how to deploy an Azure AD-enabled cluster and create a simple RBAC role in the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="1e20f-107">This article shows you how to deploy the prerequisites for AKS and Azure AD, then how to deploy an Azure AD-enabled cluster and create a simple RBAC role in the AKS cluster.</span></span>

<span data-ttu-id="1e20f-108">The following limitations apply:</span><span class="sxs-lookup"><span data-stu-id="1e20f-108">The following limitations apply:</span></span>

- <span data-ttu-id="1e20f-109">Existing non-RBAC enabled AKS clusters cannot currently be updated for RBAC use.</span><span class="sxs-lookup"><span data-stu-id="1e20f-109">Existing non-RBAC enabled AKS clusters cannot currently be updated for RBAC use.</span></span>
- <span data-ttu-id="1e20f-110">*Guest* users in Azure AD, such as if you are using a federated login from a different directory, are not supported.</span><span class="sxs-lookup"><span data-stu-id="1e20f-110">*Guest* users in Azure AD, such as if you are using a federated login from a different directory, are not supported.</span></span>

## <a name="authentication-details"></a><span data-ttu-id="1e20f-111">Authentication details</span><span class="sxs-lookup"><span data-stu-id="1e20f-111">Authentication details</span></span>

<span data-ttu-id="1e20f-112">Azure AD authentication is provided to AKS clusters with OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="1e20f-112">Azure AD authentication is provided to AKS clusters with OpenID Connect.</span></span> <span data-ttu-id="1e20f-113">OpenID Connect is an identity layer built on top of the OAuth 2.0 protocol.</span><span class="sxs-lookup"><span data-stu-id="1e20f-113">OpenID Connect is an identity layer built on top of the OAuth 2.0 protocol.</span></span> <span data-ttu-id="1e20f-114">For more information on OpenID Connect, see the [Open ID connect documentation][open-id-connect].</span><span class="sxs-lookup"><span data-stu-id="1e20f-114">For more information on OpenID Connect, see the [Open ID connect documentation][open-id-connect].</span></span>

<span data-ttu-id="1e20f-115">From inside of the Kubernetes cluster, Webhook Token Authentication is used to verify authentication tokens.</span><span class="sxs-lookup"><span data-stu-id="1e20f-115">From inside of the Kubernetes cluster, Webhook Token Authentication is used to verify authentication tokens.</span></span> <span data-ttu-id="1e20f-116">Webhook token authentication is configured and managed as part of the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="1e20f-116">Webhook token authentication is configured and managed as part of the AKS cluster.</span></span> <span data-ttu-id="1e20f-117">For more information on Webhook token authentication, see the [webhook authentication documentation][kubernetes-webhook].</span><span class="sxs-lookup"><span data-stu-id="1e20f-117">For more information on Webhook token authentication, see the [webhook authentication documentation][kubernetes-webhook].</span></span>

> [!NOTE]
> <span data-ttu-id="1e20f-118">When configuring Azure AD for AKS authentication, two Azure AD application are configured.</span><span class="sxs-lookup"><span data-stu-id="1e20f-118">When configuring Azure AD for AKS authentication, two Azure AD application are configured.</span></span> <span data-ttu-id="1e20f-119">This operation must be completed by an Azure tenant administrator.</span><span class="sxs-lookup"><span data-stu-id="1e20f-119">This operation must be completed by an Azure tenant administrator.</span></span>

## <a name="create-server-application"></a><span data-ttu-id="1e20f-120">Create server application</span><span class="sxs-lookup"><span data-stu-id="1e20f-120">Create server application</span></span>

<span data-ttu-id="1e20f-121">The first Azure AD application is used to get a users Azure AD group membership.</span><span class="sxs-lookup"><span data-stu-id="1e20f-121">The first Azure AD application is used to get a users Azure AD group membership.</span></span>

1. <span data-ttu-id="1e20f-122">Select **Azure Active Directory** > **App registrations** > **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="1e20f-122">Select **Azure Active Directory** > **App registrations** > **New application registration**.</span></span>

  <span data-ttu-id="1e20f-123">Give the application a name, select **Web app / API** for the application type, and enter any URI formatted value for **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="1e20f-123">Give the application a name, select **Web app / API** for the application type, and enter any URI formatted value for **Sign-on URL**.</span></span> <span data-ttu-id="1e20f-124">Select **Create** when done.</span><span class="sxs-lookup"><span data-stu-id="1e20f-124">Select **Create** when done.</span></span>

  ![Create Azure AD registration](media/aad-integration/app-registration.png)

2. <span data-ttu-id="1e20f-126">Select **Manifest** and edit the `groupMembershipClaims` value to `"All"`.</span><span class="sxs-lookup"><span data-stu-id="1e20f-126">Select **Manifest** and edit the `groupMembershipClaims` value to `"All"`.</span></span>

  <span data-ttu-id="1e20f-127">Save the updates once complete.</span><span class="sxs-lookup"><span data-stu-id="1e20f-127">Save the updates once complete.</span></span>

  ![Update group membership to all](media/aad-integration/edit-manifest.png)

3. <span data-ttu-id="1e20f-129">Back on the Azure AD application, select **Settings** > **Keys**.</span><span class="sxs-lookup"><span data-stu-id="1e20f-129">Back on the Azure AD application, select **Settings** > **Keys**.</span></span>

  <span data-ttu-id="1e20f-130">Add a key description, select an expiration deadline, and select **Save**.</span><span class="sxs-lookup"><span data-stu-id="1e20f-130">Add a key description, select an expiration deadline, and select **Save**.</span></span> <span data-ttu-id="1e20f-131">Take note of the key value.</span><span class="sxs-lookup"><span data-stu-id="1e20f-131">Take note of the key value.</span></span> <span data-ttu-id="1e20f-132">When deploying an Azure AD enabled AKS cluster, this value is referred to as the `Server application secret`.</span><span class="sxs-lookup"><span data-stu-id="1e20f-132">When deploying an Azure AD enabled AKS cluster, this value is referred to as the `Server application secret`.</span></span>

  ![Get the application private key](media/aad-integration/application-key.png)

4. <span data-ttu-id="1e20f-134">Return to the Azure AD application, select **Settings** > **Required permissions** > **Add** > **Select an API** > **Microsoft Graph** > **Select**.</span><span class="sxs-lookup"><span data-stu-id="1e20f-134">Return to the Azure AD application, select **Settings** > **Required permissions** > **Add** > **Select an API** > **Microsoft Graph** > **Select**.</span></span>

  ![Select graph API](media/aad-integration/graph-api.png)

5. <span data-ttu-id="1e20f-136">Under **APPLICATION PERMISSIONS** place a check next to **Read directory data**.</span><span class="sxs-lookup"><span data-stu-id="1e20f-136">Under **APPLICATION PERMISSIONS** place a check next to **Read directory data**.</span></span>

  ![Set application graph permissions](media/aad-integration/read-directory.png)

6. <span data-ttu-id="1e20f-138">Under **DELEGATED PERMISSIONS**, place a check next to **Sign in and read user profile** and **Read directory data**.</span><span class="sxs-lookup"><span data-stu-id="1e20f-138">Under **DELEGATED PERMISSIONS**, place a check next to **Sign in and read user profile** and **Read directory data**.</span></span> <span data-ttu-id="1e20f-139">Save the updates once done.</span><span class="sxs-lookup"><span data-stu-id="1e20f-139">Save the updates once done.</span></span>

  ![Set application graph permissions](media/aad-integration/delegated-permissions.png)

7. <span data-ttu-id="1e20f-141">Select **Done**, choose *Microsoft Graph* from the list of APIs, then select **Grant Permissions**.</span><span class="sxs-lookup"><span data-stu-id="1e20f-141">Select **Done**, choose *Microsoft Graph* from the list of APIs, then select **Grant Permissions**.</span></span> <span data-ttu-id="1e20f-142">This step will fail if the current account is not a tenant admin.</span><span class="sxs-lookup"><span data-stu-id="1e20f-142">This step will fail if the current account is not a tenant admin.</span></span>

  ![Set application graph permissions](media/aad-integration/grant-permissions.png)

  <span data-ttu-id="1e20f-144">When the permissions have been successfully granted, the following notification is displayed in the portal:</span><span class="sxs-lookup"><span data-stu-id="1e20f-144">When the permissions have been successfully granted, the following notification is displayed in the portal:</span></span>

  ![Notification of successful permissions granted](media/aad-integration/permissions-granted.png)

8. <span data-ttu-id="1e20f-146">Return to the application and take note of the **Application ID**.</span><span class="sxs-lookup"><span data-stu-id="1e20f-146">Return to the application and take note of the **Application ID**.</span></span> <span data-ttu-id="1e20f-147">When deploying an Azure AD-enabled AKS cluster, this value is referred to as the `Server application ID`.</span><span class="sxs-lookup"><span data-stu-id="1e20f-147">When deploying an Azure AD-enabled AKS cluster, this value is referred to as the `Server application ID`.</span></span>

  ![Get application ID](media/aad-integration/application-id.png)

## <a name="create-client-application"></a><span data-ttu-id="1e20f-149">Create client application</span><span class="sxs-lookup"><span data-stu-id="1e20f-149">Create client application</span></span>

<span data-ttu-id="1e20f-150">The second Azure AD application is used when logging in with the Kubernetes CLI (kubectl.)</span><span class="sxs-lookup"><span data-stu-id="1e20f-150">The second Azure AD application is used when logging in with the Kubernetes CLI (kubectl.)</span></span>

1. <span data-ttu-id="1e20f-151">Select **Azure Active Directory** > **App registrations** > **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="1e20f-151">Select **Azure Active Directory** > **App registrations** > **New application registration**.</span></span>

  <span data-ttu-id="1e20f-152">Give the application a name, select **Native** for the application type, and enter any URI formatted value for **Redirect URI**.</span><span class="sxs-lookup"><span data-stu-id="1e20f-152">Give the application a name, select **Native** for the application type, and enter any URI formatted value for **Redirect URI**.</span></span> <span data-ttu-id="1e20f-153">Select **Create** when done.</span><span class="sxs-lookup"><span data-stu-id="1e20f-153">Select **Create** when done.</span></span>

  ![Create AAD registration](media/aad-integration/app-registration-client.png)

2. <span data-ttu-id="1e20f-155">From the Azure AD application, select **Settings** > **Required permissions** > **Add** > **Select an API** and search for the name of the server application created in the last step of this document.</span><span class="sxs-lookup"><span data-stu-id="1e20f-155">From the Azure AD application, select **Settings** > **Required permissions** > **Add** > **Select an API** and search for the name of the server application created in the last step of this document.</span></span>

  ![Configure application permissions](media/aad-integration/select-api.png)

3. <span data-ttu-id="1e20f-157">Place a check mark next to the application and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="1e20f-157">Place a check mark next to the application and click **Select**.</span></span>

  ![Select AKS AAD server application endpoint](media/aad-integration/select-server-app.png)

4. <span data-ttu-id="1e20f-159">Select **Done** and **Grant Permissions** to complete this step.</span><span class="sxs-lookup"><span data-stu-id="1e20f-159">Select **Done** and **Grant Permissions** to complete this step.</span></span>

  ![Grant permissions](media/aad-integration/grant-permissions-client.png)

5. <span data-ttu-id="1e20f-161">Back on the AD application, take note of the **Application ID**.</span><span class="sxs-lookup"><span data-stu-id="1e20f-161">Back on the AD application, take note of the **Application ID**.</span></span> <span data-ttu-id="1e20f-162">When deploying an Azure AD-enabled AKS cluster, this value is referred to as the `Client application ID`.</span><span class="sxs-lookup"><span data-stu-id="1e20f-162">When deploying an Azure AD-enabled AKS cluster, this value is referred to as the `Client application ID`.</span></span>

  ![Get the application ID](media/aad-integration/application-id-client.png)

## <a name="get-tenant-id"></a><span data-ttu-id="1e20f-164">Get tenant ID</span><span class="sxs-lookup"><span data-stu-id="1e20f-164">Get tenant ID</span></span>

<span data-ttu-id="1e20f-165">Finally, get the ID of your Azure tenant.</span><span class="sxs-lookup"><span data-stu-id="1e20f-165">Finally, get the ID of your Azure tenant.</span></span> <span data-ttu-id="1e20f-166">This value is also used when deploying the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="1e20f-166">This value is also used when deploying the AKS cluster.</span></span>

<span data-ttu-id="1e20f-167">From the Azure portal, select **Azure Active Directory** > **Properties** and take note of the **Directory ID**.</span><span class="sxs-lookup"><span data-stu-id="1e20f-167">From the Azure portal, select **Azure Active Directory** > **Properties** and take note of the **Directory ID**.</span></span> <span data-ttu-id="1e20f-168">When deploying an Azure AD-enabled AKS cluster, this value is referred to as the `Tenant ID`.</span><span class="sxs-lookup"><span data-stu-id="1e20f-168">When deploying an Azure AD-enabled AKS cluster, this value is referred to as the `Tenant ID`.</span></span>

![Get the Azure tenant ID](media/aad-integration/tenant-id.png)

## <a name="deploy-cluster"></a><span data-ttu-id="1e20f-170">Deploy Cluster</span><span class="sxs-lookup"><span data-stu-id="1e20f-170">Deploy Cluster</span></span>

<span data-ttu-id="1e20f-171">Use the [az group create][az-group-create] command to create a resource group for the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="1e20f-171">Use the [az group create][az-group-create] command to create a resource group for the AKS cluster.</span></span>

```azurecli
az group create --name myAKSCluster --location eastus
```

<span data-ttu-id="1e20f-172">Deploy the cluster using the [az aks create][az-aks-create] command.</span><span class="sxs-lookup"><span data-stu-id="1e20f-172">Deploy the cluster using the [az aks create][az-aks-create] command.</span></span> <span data-ttu-id="1e20f-173">Replace the values in the sample command below with the values collected when creating the Azure AD applications.</span><span class="sxs-lookup"><span data-stu-id="1e20f-173">Replace the values in the sample command below with the values collected when creating the Azure AD applications.</span></span>

```azurecli
az aks create --resource-group myAKSCluster --name myAKSCluster --generate-ssh-keys --enable-rbac \
  --aad-server-app-id b1536b67-29ab-4b63-b60f-9444d0c15df1 \
  --aad-server-app-secret wHYomLe2i1mHR2B3/d4sFrooHwADZccKwfoQwK2QHg= \
  --aad-client-app-id 8aaf8bd5-1bdd-4822-99ad-02bfaa63eea7 \
  --aad-tenant-id 72f988bf-0000-0000-0000-2d7cd011db47
```

## <a name="create-rbac-binding"></a><span data-ttu-id="1e20f-174">Create RBAC binding</span><span class="sxs-lookup"><span data-stu-id="1e20f-174">Create RBAC binding</span></span>

<span data-ttu-id="1e20f-175">Before an Azure Active Directory account can be used with the AKS cluster, a role binding or cluster role binding needs to be created.</span><span class="sxs-lookup"><span data-stu-id="1e20f-175">Before an Azure Active Directory account can be used with the AKS cluster, a role binding or cluster role binding needs to be created.</span></span> <span data-ttu-id="1e20f-176">*Roles* define the permissions to grant, and *bindings* apply them to desired users.</span><span class="sxs-lookup"><span data-stu-id="1e20f-176">*Roles* define the permissions to grant, and *bindings* apply them to desired users.</span></span> <span data-ttu-id="1e20f-177">These assignments can be applied to a given namespace, or across the entire cluster.</span><span class="sxs-lookup"><span data-stu-id="1e20f-177">These assignments can be applied to a given namespace, or across the entire cluster.</span></span> <span data-ttu-id="1e20f-178">For more information, see [Using RBAC authorization][rbac-authorization].</span><span class="sxs-lookup"><span data-stu-id="1e20f-178">For more information, see [Using RBAC authorization][rbac-authorization].</span></span>

<span data-ttu-id="1e20f-179">First, use the [az aks get-credentials][az-aks-get-credentials] command with the `--admin` argument to log in to the cluster with admin access.</span><span class="sxs-lookup"><span data-stu-id="1e20f-179">First, use the [az aks get-credentials][az-aks-get-credentials] command with the `--admin` argument to log in to the cluster with admin access.</span></span>

```azurecli
az aks get-credentials --resource-group myAKSCluster --name myAKSCluster --admin
```

<span data-ttu-id="1e20f-180">Next, use the following manifest to create a ClusterRoleBinding for an Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="1e20f-180">Next, use the following manifest to create a ClusterRoleBinding for an Azure AD account.</span></span> <span data-ttu-id="1e20f-181">Update the user name with one from your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="1e20f-181">Update the user name with one from your Azure AD tenant.</span></span> <span data-ttu-id="1e20f-182">This example gives the account full access to all namespaces of the cluster:</span><span class="sxs-lookup"><span data-stu-id="1e20f-182">This example gives the account full access to all namespaces of the cluster:</span></span>

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: contoso-cluster-admins
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- apiGroup: rbac.authorization.k8s.io
  kind: User
  name: "user@contoso.com"
```

<span data-ttu-id="1e20f-183">A role binding can also be created for all members of an Azure AD group.</span><span class="sxs-lookup"><span data-stu-id="1e20f-183">A role binding can also be created for all members of an Azure AD group.</span></span> <span data-ttu-id="1e20f-184">Azure AD groups are specified using the group object ID, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="1e20f-184">Azure AD groups are specified using the group object ID, as shown in the following example:</span></span>

 ```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: contoso-cluster-admins
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- apiGroup: rbac.authorization.k8s.io
   kind: Group
   name: "894656e1-39f8-4bfe-b16a-510f61af6f41"
```

<span data-ttu-id="1e20f-185">For more information on securing a Kubernetes cluster with RBAC, see [Using RBAC Authorization][rbac-authorization].</span><span class="sxs-lookup"><span data-stu-id="1e20f-185">For more information on securing a Kubernetes cluster with RBAC, see [Using RBAC Authorization][rbac-authorization].</span></span>

## <a name="access-cluster-with-azure-ad"></a><span data-ttu-id="1e20f-186">Access cluster with Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e20f-186">Access cluster with Azure AD</span></span>

<span data-ttu-id="1e20f-187">Next, pull the context for the non-admin user using the [az aks get-credentials][az-aks-get-credentials] command.</span><span class="sxs-lookup"><span data-stu-id="1e20f-187">Next, pull the context for the non-admin user using the [az aks get-credentials][az-aks-get-credentials] command.</span></span>

```azurecli
az aks get-credentials --resource-group myAKSCluster --name myAKSCluster
```

<span data-ttu-id="1e20f-188">After running any kubectl command, you will be prompted to authenticate with Azure.</span><span class="sxs-lookup"><span data-stu-id="1e20f-188">After running any kubectl command, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="1e20f-189">Follow the on-screen instructions.</span><span class="sxs-lookup"><span data-stu-id="1e20f-189">Follow the on-screen instructions.</span></span>

```console
$ kubectl get nodes

To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code BUJHWDGNL to authenticate.

NAME                       STATUS    ROLES     AGE       VERSION
aks-nodepool1-42032720-0   Ready     agent     1h        v1.9.6
aks-nodepool1-42032720-1   Ready     agent     1h        v1.9.6
aks-nodepool1-42032720-2   Ready     agent     1h        v1.9.6
```

<span data-ttu-id="1e20f-190">Once complete, the authentication token is cached.</span><span class="sxs-lookup"><span data-stu-id="1e20f-190">Once complete, the authentication token is cached.</span></span> <span data-ttu-id="1e20f-191">You are only reprompted to log in when the token has expired or the Kubernetes config file re-created.</span><span class="sxs-lookup"><span data-stu-id="1e20f-191">You are only reprompted to log in when the token has expired or the Kubernetes config file re-created.</span></span>

<span data-ttu-id="1e20f-192">If you are seeing an authorization error message after signing in successfully, check that the user you are signing in as is not a Guest in the Azure AD (this is often the case if you are using a federated login from a different directory).</span><span class="sxs-lookup"><span data-stu-id="1e20f-192">If you are seeing an authorization error message after signing in successfully, check that the user you are signing in as is not a Guest in the Azure AD (this is often the case if you are using a federated login from a different directory).</span></span>
```console
error: You must be logged in to the server (Unauthorized)
```


## <a name="next-steps"></a><span data-ttu-id="1e20f-193">Next Steps</span><span class="sxs-lookup"><span data-stu-id="1e20f-193">Next Steps</span></span>

<span data-ttu-id="1e20f-194">Learn more about securing Kubernetes clusters with RBAC with the [Using RBAC Authorization][rbac-authorization] documentation.</span><span class="sxs-lookup"><span data-stu-id="1e20f-194">Learn more about securing Kubernetes clusters with RBAC with the [Using RBAC Authorization][rbac-authorization] documentation.</span></span>

<!-- LINKS - external -->
[kubernetes-webhook]:https://kubernetes.io/docs/reference/access-authn-authz/authentication/#webhook-token-authentication
[rbac-authorization]: https://kubernetes.io/docs/reference/access-authn-authz/rbac/

<!-- LINKS - internal -->
[az-aks-create]: /cli/azure/aks?view=azure-cli-latest#az-aks-create
[az-aks-get-credentials]: /cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials
[az-group-create]: /cli/azure/group#az-group-create
[open-id-connect]:../active-directory/develop/v1-protocols-openid-connect-code.md
