---
title: Use Draft with AKS and Azure Container Registry
description: Use Draft with AKS and Azure Container Registry
services: container-service
author: iainfoulds
ms.service: container-service
ms.topic: article
ms.date: 08/15/2018
ms.author: iainfou
ms.openlocfilehash: 15fbf254eb479f0935e154806795ebd00cff6adf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857965"
---
# <a name="use-draft-with-azure-kubernetes-service-aks"></a><span data-ttu-id="b8efc-103">Use Draft with Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="b8efc-103">Use Draft with Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="b8efc-104">Draft is an open-source tool that helps package and deploy application containers in a Kubernetes cluster, leaving you free to concentrate on the dev cycle - the "inner loop" of concentrated development.</span><span class="sxs-lookup"><span data-stu-id="b8efc-104">Draft is an open-source tool that helps package and deploy application containers in a Kubernetes cluster, leaving you free to concentrate on the dev cycle - the "inner loop" of concentrated development.</span></span> <span data-ttu-id="b8efc-105">Draft works as the code is being developed, but before committing to version control.</span><span class="sxs-lookup"><span data-stu-id="b8efc-105">Draft works as the code is being developed, but before committing to version control.</span></span> <span data-ttu-id="b8efc-106">With Draft, you can quickly redeploy an application to Kubernetes as code changes occur.</span><span class="sxs-lookup"><span data-stu-id="b8efc-106">With Draft, you can quickly redeploy an application to Kubernetes as code changes occur.</span></span> <span data-ttu-id="b8efc-107">For more information on Draft, see the [Draft documentation on Github][draft-documentation].</span><span class="sxs-lookup"><span data-stu-id="b8efc-107">For more information on Draft, see the [Draft documentation on Github][draft-documentation].</span></span>

<span data-ttu-id="b8efc-108">This article shows you how to use Draft with a Kubernetes cluster on AKS.</span><span class="sxs-lookup"><span data-stu-id="b8efc-108">This article shows you how to use Draft with a Kubernetes cluster on AKS.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8efc-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b8efc-109">Prerequisites</span></span>

<span data-ttu-id="b8efc-110">The steps detailed in this article assume that you have created an AKS cluster and have established a `kubectl` connection with the cluster.</span><span class="sxs-lookup"><span data-stu-id="b8efc-110">The steps detailed in this article assume that you have created an AKS cluster and have established a `kubectl` connection with the cluster.</span></span> <span data-ttu-id="b8efc-111">If you need these items, see the [AKS quickstart][aks-quickstart].</span><span class="sxs-lookup"><span data-stu-id="b8efc-111">If you need these items, see the [AKS quickstart][aks-quickstart].</span></span>

<span data-ttu-id="b8efc-112">You need a private Docker registry in Azure Container Registry (ACR).</span><span class="sxs-lookup"><span data-stu-id="b8efc-112">You need a private Docker registry in Azure Container Registry (ACR).</span></span> <span data-ttu-id="b8efc-113">For steps on how to create an ACR instance, see the [Azure Container Registry quickstart][acr-quickstart].</span><span class="sxs-lookup"><span data-stu-id="b8efc-113">For steps on how to create an ACR instance, see the [Azure Container Registry quickstart][acr-quickstart].</span></span>

<span data-ttu-id="b8efc-114">Helm must also be installed in your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="b8efc-114">Helm must also be installed in your AKS cluster.</span></span> <span data-ttu-id="b8efc-115">For more information on how to install and configure Helm, see [Use Helm with Azure Kubernetes Service (AKS)][aks-helm].</span><span class="sxs-lookup"><span data-stu-id="b8efc-115">For more information on how to install and configure Helm, see [Use Helm with Azure Kubernetes Service (AKS)][aks-helm].</span></span>

<span data-ttu-id="b8efc-116">Finally, you must install [Docker](https://www.docker.com).</span><span class="sxs-lookup"><span data-stu-id="b8efc-116">Finally, you must install [Docker](https://www.docker.com).</span></span>

## <a name="install-draft"></a><span data-ttu-id="b8efc-117">Install Draft</span><span class="sxs-lookup"><span data-stu-id="b8efc-117">Install Draft</span></span>

<span data-ttu-id="b8efc-118">The Draft CLI is a client that runs on your development system and allows you to deploy code into a Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="b8efc-118">The Draft CLI is a client that runs on your development system and allows you to deploy code into a Kubernetes cluster.</span></span> <span data-ttu-id="b8efc-119">To install the Draft CLI on a Mac, use `brew`.</span><span class="sxs-lookup"><span data-stu-id="b8efc-119">To install the Draft CLI on a Mac, use `brew`.</span></span> <span data-ttu-id="b8efc-120">For additional installation options, see the [Draft Install guide][draft-documentation].</span><span class="sxs-lookup"><span data-stu-id="b8efc-120">For additional installation options, see the [Draft Install guide][draft-documentation].</span></span>

> [!NOTE]
> <span data-ttu-id="b8efc-121">If you installed Draft prior to version 0.12, first delete Draft from your cluster using `helm delete --purge draft` and then remove your local configuration by running `rm -rf ~/.draft`.</span><span class="sxs-lookup"><span data-stu-id="b8efc-121">If you installed Draft prior to version 0.12, first delete Draft from your cluster using `helm delete --purge draft` and then remove your local configuration by running `rm -rf ~/.draft`.</span></span> <span data-ttu-id="b8efc-122">If you are on MacOS, then run `brew upgrade draft`.</span><span class="sxs-lookup"><span data-stu-id="b8efc-122">If you are on MacOS, then run `brew upgrade draft`.</span></span>

```console
brew tap azure/draft
brew install draft
```

<span data-ttu-id="b8efc-123">Now initialize Draft with the `draft init` command:</span><span class="sxs-lookup"><span data-stu-id="b8efc-123">Now initialize Draft with the `draft init` command:</span></span>

```console
draft init
```

## <a name="configure-draft"></a><span data-ttu-id="b8efc-124">Configure Draft</span><span class="sxs-lookup"><span data-stu-id="b8efc-124">Configure Draft</span></span>

<span data-ttu-id="b8efc-125">Draft builds the container images locally, and then either deploys them from the local registry (such as with Minikube), or uses an image registry that you specify.</span><span class="sxs-lookup"><span data-stu-id="b8efc-125">Draft builds the container images locally, and then either deploys them from the local registry (such as with Minikube), or uses an image registry that you specify.</span></span> <span data-ttu-id="b8efc-126">This article uses Azure Container Registry (ACR), so you must establish a trust relationship between your AKS cluster and the ACR registry, then configure Draft to push your container images to ACR.</span><span class="sxs-lookup"><span data-stu-id="b8efc-126">This article uses Azure Container Registry (ACR), so you must establish a trust relationship between your AKS cluster and the ACR registry, then configure Draft to push your container images to ACR.</span></span>

### <a name="create-trust-between-aks-cluster-and-acr"></a><span data-ttu-id="b8efc-127">Create trust between AKS cluster and ACR</span><span class="sxs-lookup"><span data-stu-id="b8efc-127">Create trust between AKS cluster and ACR</span></span>

<span data-ttu-id="b8efc-128">To establish trust between an AKS cluster and an ACR registry, grant permissions for the Azure Active Directory service principal used by the AKS cluster to access the ACR registry.</span><span class="sxs-lookup"><span data-stu-id="b8efc-128">To establish trust between an AKS cluster and an ACR registry, grant permissions for the Azure Active Directory service principal used by the AKS cluster to access the ACR registry.</span></span> <span data-ttu-id="b8efc-129">In the following commands, provide your own `<resourceGroupName>`, replace `<aksName>` with name of your AKS cluster, and replace `<acrName>` with the name of your ACR registry:</span><span class="sxs-lookup"><span data-stu-id="b8efc-129">In the following commands, provide your own `<resourceGroupName>`, replace `<aksName>` with name of your AKS cluster, and replace `<acrName>` with the name of your ACR registry:</span></span>

```azurecli
# Get the service principal ID of your AKS cluster
AKS_SP_ID=$(az aks show --resource-group <resourceGroupName> --name <aksName> --query "servicePrincipalProfile.clientId" -o tsv)

# Get the resource ID of your ACR instance
ACR_RESOURCE_ID=$(az acr show --resource-group <resourceGroupName> --name <acrName> --query "id" -o tsv)

# Create a role assignment for your AKS cluster to access the ACR instance
az role assignment create --assignee $AKS_SP_ID --scope $ACR_RESOURCE_ID --role contributor
```

<span data-ttu-id="b8efc-130">For more information on these steps to access ACR, see [authenticating with ACR](../container-registry/container-registry-auth-aks.md).</span><span class="sxs-lookup"><span data-stu-id="b8efc-130">For more information on these steps to access ACR, see [authenticating with ACR](../container-registry/container-registry-auth-aks.md).</span></span>

### <a name="configure-draft-to-push-to-and-deploy-from-acr"></a><span data-ttu-id="b8efc-131">Configure Draft to push to and deploy from ACR</span><span class="sxs-lookup"><span data-stu-id="b8efc-131">Configure Draft to push to and deploy from ACR</span></span>

<span data-ttu-id="b8efc-132">Now that there is a trust relationship between AKS and ACR, enable the use of ACR from your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="b8efc-132">Now that there is a trust relationship between AKS and ACR, enable the use of ACR from your AKS cluster.</span></span>

1. <span data-ttu-id="b8efc-133">Set the Draft configuration *registry* value.</span><span class="sxs-lookup"><span data-stu-id="b8efc-133">Set the Draft configuration *registry* value.</span></span> <span data-ttu-id="b8efc-134">In the following commands, replace `<acrName>` with the name of your ACR registry:</span><span class="sxs-lookup"><span data-stu-id="b8efc-134">In the following commands, replace `<acrName>` with the name of your ACR registry:</span></span>

    ```console
    draft config set registry <acrName>.azurecr.io
    ```

1. <span data-ttu-id="b8efc-135">Log on to the ACR registry with [az acr login][az-acr-login]:</span><span class="sxs-lookup"><span data-stu-id="b8efc-135">Log on to the ACR registry with [az acr login][az-acr-login]:</span></span>

    ```azurecli
    az acr login --name <acrName>
    ```

<span data-ttu-id="b8efc-136">As a trust was created between AKS and ACR, no passwords or secrets are required to push to or pull from the ACR registry.</span><span class="sxs-lookup"><span data-stu-id="b8efc-136">As a trust was created between AKS and ACR, no passwords or secrets are required to push to or pull from the ACR registry.</span></span> <span data-ttu-id="b8efc-137">Authentication happens at the Azure Resource Manager level, using Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b8efc-137">Authentication happens at the Azure Resource Manager level, using Azure Active Directory.</span></span>

## <a name="run-an-application"></a><span data-ttu-id="b8efc-138">Run an application</span><span class="sxs-lookup"><span data-stu-id="b8efc-138">Run an application</span></span>

<span data-ttu-id="b8efc-139">To see Draft in action, let's deploy a sample application from the [Draft repository][draft-repo].</span><span class="sxs-lookup"><span data-stu-id="b8efc-139">To see Draft in action, let's deploy a sample application from the [Draft repository][draft-repo].</span></span> <span data-ttu-id="b8efc-140">First, clone the repo:</span><span class="sxs-lookup"><span data-stu-id="b8efc-140">First, clone the repo:</span></span>

```console
git clone https://github.com/Azure/draft
```

<span data-ttu-id="b8efc-141">Change to the Java examples directory:</span><span class="sxs-lookup"><span data-stu-id="b8efc-141">Change to the Java examples directory:</span></span>

```console
cd draft/examples/example-java/
```

<span data-ttu-id="b8efc-142">Use the `draft create` command to start the process.</span><span class="sxs-lookup"><span data-stu-id="b8efc-142">Use the `draft create` command to start the process.</span></span> <span data-ttu-id="b8efc-143">This command creates the artifacts that are used to run the application in a Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="b8efc-143">This command creates the artifacts that are used to run the application in a Kubernetes cluster.</span></span> <span data-ttu-id="b8efc-144">These items include a Dockerfile, a Helm chart, and a *draft.toml* file, which is the Draft configuration file.</span><span class="sxs-lookup"><span data-stu-id="b8efc-144">These items include a Dockerfile, a Helm chart, and a *draft.toml* file, which is the Draft configuration file.</span></span>

```
$ draft create

--> Draft detected Java (92.205567%)
--> Ready to sail
```

<span data-ttu-id="b8efc-145">To run the sample application in your AKS cluster, use the `draft up` command.</span><span class="sxs-lookup"><span data-stu-id="b8efc-145">To run the sample application in your AKS cluster, use the `draft up` command.</span></span> <span data-ttu-id="b8efc-146">This command builds the Dockerfile to create a container image, pushes the image to ACR, and finally installs the Helm chart to start the application in AKS.</span><span class="sxs-lookup"><span data-stu-id="b8efc-146">This command builds the Dockerfile to create a container image, pushes the image to ACR, and finally installs the Helm chart to start the application in AKS.</span></span>

<span data-ttu-id="b8efc-147">The first time this command is run, pushing and pulling the container image may take some time.</span><span class="sxs-lookup"><span data-stu-id="b8efc-147">The first time this command is run, pushing and pulling the container image may take some time.</span></span> <span data-ttu-id="b8efc-148">Once the base layers are cached, the time taken to deploy the application is dramatically reduced.</span><span class="sxs-lookup"><span data-stu-id="b8efc-148">Once the base layers are cached, the time taken to deploy the application is dramatically reduced.</span></span>

```
$ draft up

Draft Up Started: 'example-java': 01CMZAR1F4T1TJZ8SWJQ70HCNH
example-java: Building Docker Image: SUCCESS ⚓  (73.0720s)
example-java: Pushing Docker Image: SUCCESS ⚓  (19.5727s)
example-java: Releasing Application: SUCCESS ⚓  (4.6979s)
Inspect the logs with `draft logs 01CMZAR1F4T1TJZ8SWJQ70HCNH`
```

<span data-ttu-id="b8efc-149">If you encounter issues pushing the Docker image, ensure that you have successfully logged in to your ACR registry with [az acr login][az-acr-login], then try the `draft up` command again.</span><span class="sxs-lookup"><span data-stu-id="b8efc-149">If you encounter issues pushing the Docker image, ensure that you have successfully logged in to your ACR registry with [az acr login][az-acr-login], then try the `draft up` command again.</span></span>

## <a name="test-the-application-locally"></a><span data-ttu-id="b8efc-150">Test the application locally</span><span class="sxs-lookup"><span data-stu-id="b8efc-150">Test the application locally</span></span>

<span data-ttu-id="b8efc-151">To test the application, use the `draft connect` command.</span><span class="sxs-lookup"><span data-stu-id="b8efc-151">To test the application, use the `draft connect` command.</span></span> <span data-ttu-id="b8efc-152">This command proxies a secure connection to the Kubernetes pod.</span><span class="sxs-lookup"><span data-stu-id="b8efc-152">This command proxies a secure connection to the Kubernetes pod.</span></span> <span data-ttu-id="b8efc-153">When complete, the application can be accessed on the provided URL.</span><span class="sxs-lookup"><span data-stu-id="b8efc-153">When complete, the application can be accessed on the provided URL.</span></span>

> [!NOTE]
> <span data-ttu-id="b8efc-154">It may take a few minutes for the container image to be downloaded and the application to start.</span><span class="sxs-lookup"><span data-stu-id="b8efc-154">It may take a few minutes for the container image to be downloaded and the application to start.</span></span> <span data-ttu-id="b8efc-155">If you receive an error when accessing the application, retry the connection.</span><span class="sxs-lookup"><span data-stu-id="b8efc-155">If you receive an error when accessing the application, retry the connection.</span></span>

```
$ draft connect

Connect to java:4567 on localhost:49804
[java]: SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
[java]: SLF4J: Defaulting to no-operation (NOP) logger implementation
[java]: SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
[java]: == Spark has ignited ...
[java]: >> Listening on 0.0.0.0:4567
```

<span data-ttu-id="b8efc-156">To access your application, open a web browser to the address and port specified in the `draft connect` output, such as *http://localhost:49804*.</span><span class="sxs-lookup"><span data-stu-id="b8efc-156">To access your application, open a web browser to the address and port specified in the `draft connect` output, such as *http://localhost:49804*.</span></span> 

![Sample Java app running with Draft](media/kubernetes-draft/sample-app.png)

<span data-ttu-id="b8efc-158">Use `Control+C` to stop the proxy connection.</span><span class="sxs-lookup"><span data-stu-id="b8efc-158">Use `Control+C` to stop the proxy connection.</span></span>

> [!NOTE]
> <span data-ttu-id="b8efc-159">You can also use the `draft up --auto-connect` command to build and deploy your application then immediately connect to the first running container.</span><span class="sxs-lookup"><span data-stu-id="b8efc-159">You can also use the `draft up --auto-connect` command to build and deploy your application then immediately connect to the first running container.</span></span>

## <a name="access-the-application-on-the-internet"></a><span data-ttu-id="b8efc-160">Access the application on the internet</span><span class="sxs-lookup"><span data-stu-id="b8efc-160">Access the application on the internet</span></span>

<span data-ttu-id="b8efc-161">The previous step created a proxy connection to the application pod in your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="b8efc-161">The previous step created a proxy connection to the application pod in your AKS cluster.</span></span> <span data-ttu-id="b8efc-162">As you develop and test your application, you may want to make the application available on the internet.</span><span class="sxs-lookup"><span data-stu-id="b8efc-162">As you develop and test your application, you may want to make the application available on the internet.</span></span> <span data-ttu-id="b8efc-163">To expose an application on the internet, you create a Kubernetes service with a type of [LoadBalancer][kubernetes-service-loadbalancer], or create an [ingress controller][kubernetes-ingress].</span><span class="sxs-lookup"><span data-stu-id="b8efc-163">To expose an application on the internet, you create a Kubernetes service with a type of [LoadBalancer][kubernetes-service-loadbalancer], or create an [ingress controller][kubernetes-ingress].</span></span> <span data-ttu-id="b8efc-164">Let's create a *LoadBalancer* service.</span><span class="sxs-lookup"><span data-stu-id="b8efc-164">Let's create a *LoadBalancer* service.</span></span>

<span data-ttu-id="b8efc-165">First, update the *values.yaml* Draft pack to specify that a service with a type *LoadBalancer* should be created:</span><span class="sxs-lookup"><span data-stu-id="b8efc-165">First, update the *values.yaml* Draft pack to specify that a service with a type *LoadBalancer* should be created:</span></span>

```console
vi charts/java/values.yaml
```

<span data-ttu-id="b8efc-166">Locate the *service.type* property and update the value from *ClusterIP* to *LoadBalancer*, as shown in the following condensed example:</span><span class="sxs-lookup"><span data-stu-id="b8efc-166">Locate the *service.type* property and update the value from *ClusterIP* to *LoadBalancer*, as shown in the following condensed example:</span></span>

```yaml
[...]
service:
  name: java
  type: LoadBalancer
  externalPort: 80
  internalPort: 4567
[...]
```

<span data-ttu-id="b8efc-167">Save and close the file, then use `draft up` to rerun the application:</span><span class="sxs-lookup"><span data-stu-id="b8efc-167">Save and close the file, then use `draft up` to rerun the application:</span></span>

```console
draft up
```

<span data-ttu-id="b8efc-168">It takes a few minutes for the service to return a public IP address.</span><span class="sxs-lookup"><span data-stu-id="b8efc-168">It takes a few minutes for the service to return a public IP address.</span></span> <span data-ttu-id="b8efc-169">To monitor the progress, use the `kubectl get service` command with the *watch* parameter:</span><span class="sxs-lookup"><span data-stu-id="b8efc-169">To monitor the progress, use the `kubectl get service` command with the *watch* parameter:</span></span>

```console
kubectl get service --watch
```

<span data-ttu-id="b8efc-170">Initially, the *EXTERNAL-IP* for the service appears as *pending*:</span><span class="sxs-lookup"><span data-stu-id="b8efc-170">Initially, the *EXTERNAL-IP* for the service appears as *pending*:</span></span>

```
NAME                TYPE          CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
example-java-java   LoadBalancer  10.0.141.72   <pending>     80:32150/TCP   2m
```

<span data-ttu-id="b8efc-171">Once the EXTERNAL-IP address has changed from *pending* to an IP address, use `Control+C` to stop the `kubectl` watch process:</span><span class="sxs-lookup"><span data-stu-id="b8efc-171">Once the EXTERNAL-IP address has changed from *pending* to an IP address, use `Control+C` to stop the `kubectl` watch process:</span></span>

```
NAME                TYPE           CLUSTER-IP    EXTERNAL-IP     PORT(S)        AGE
example-java-java   LoadBalancer   10.0.141.72   52.175.224.118  80:32150/TCP   7m
```

<span data-ttu-id="b8efc-172">To see the application, browse to the external IP address of your load balancer with `curl`:</span><span class="sxs-lookup"><span data-stu-id="b8efc-172">To see the application, browse to the external IP address of your load balancer with `curl`:</span></span>

```
$ curl 52.175.224.118

Hello World, I'm Java
```

## <a name="iterate-on-the-application"></a><span data-ttu-id="b8efc-173">Iterate on the application</span><span class="sxs-lookup"><span data-stu-id="b8efc-173">Iterate on the application</span></span>

<span data-ttu-id="b8efc-174">Now that Draft has been configured and the application is running in Kubernetes, you are set for code iteration.</span><span class="sxs-lookup"><span data-stu-id="b8efc-174">Now that Draft has been configured and the application is running in Kubernetes, you are set for code iteration.</span></span> <span data-ttu-id="b8efc-175">Each time you want to test updated code, run the `draft up` command to update the running application.</span><span class="sxs-lookup"><span data-stu-id="b8efc-175">Each time you want to test updated code, run the `draft up` command to update the running application.</span></span>

<span data-ttu-id="b8efc-176">In this example, update the Java sample application to change the display text.</span><span class="sxs-lookup"><span data-stu-id="b8efc-176">In this example, update the Java sample application to change the display text.</span></span> <span data-ttu-id="b8efc-177">Open the *Hello.java* file:</span><span class="sxs-lookup"><span data-stu-id="b8efc-177">Open the *Hello.java* file:</span></span>

```console
vi src/main/java/helloworld/Hello.java
```

<span data-ttu-id="b8efc-178">Update the output text to display, *Hello World, I'm Java in AKS!*:</span><span class="sxs-lookup"><span data-stu-id="b8efc-178">Update the output text to display, *Hello World, I'm Java in AKS!*:</span></span>

```java
package helloworld;

import static spark.Spark.*;

public class Hello {
    public static void main(String[] args) {
        get("/", (req, res) -> "Hello World, I'm Java in AKS!");
    }
}
```

<span data-ttu-id="b8efc-179">Run the `draft up` command to redeploy the application:</span><span class="sxs-lookup"><span data-stu-id="b8efc-179">Run the `draft up` command to redeploy the application:</span></span>

```console
$ draft up

Draft Up Started: 'example-java': 01CMZC9RF0TZT7XPWGFCJE15X4
example-java: Building Docker Image: SUCCESS ⚓  (25.0202s)
example-java: Pushing Docker Image: SUCCESS ⚓  (7.1457s)
example-java: Releasing Application: SUCCESS ⚓  (3.5773s)
Inspect the logs with `draft logs 01CMZC9RF0TZT7XPWGFCJE15X4`
```

<span data-ttu-id="b8efc-180">To see the updated application, curl the IP address of your load balancer again:</span><span class="sxs-lookup"><span data-stu-id="b8efc-180">To see the updated application, curl the IP address of your load balancer again:</span></span>

```
$ curl 52.175.224.118

Hello World, I'm Java in AKS!
```

## <a name="next-steps"></a><span data-ttu-id="b8efc-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="b8efc-181">Next steps</span></span>

<span data-ttu-id="b8efc-182">For more information about using Draft, see the Draft documentation on GitHub.</span><span class="sxs-lookup"><span data-stu-id="b8efc-182">For more information about using Draft, see the Draft documentation on GitHub.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="b8efc-183">[Draft documentation][draft-documentation]</span><span class="sxs-lookup"><span data-stu-id="b8efc-183">[Draft documentation][draft-documentation]</span></span>

<!-- LINKS - external -->
[draft-documentation]: https://github.com/Azure/draft/tree/master/docs
[kubernetes-service-loadbalancer]: https://kubernetes.io/docs/concepts/services-networking/service/#type-loadbalancer
[draft-repo]: https://github.com/Azure/draft

<!-- LINKS - internal -->
[acr-quickstart]: ../container-registry/container-registry-get-started-azure-cli.md
[aks-helm]: ./kubernetes-helm.md
[kubernetes-ingress]: ./ingress-basic.md
[aks-quickstart]: ./kubernetes-walkthrough.md
[az-acr-login]: /cli/azure/acr#az-acr-login
