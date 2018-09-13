---
title: Create an ingress controller for an internal network in Azure Kubernetes Service (AKS)
description: Learn how to install and configure an NGINX ingress controller for an internal, private network in an Azure Kubernetes Service (AKS) cluster.
services: container-service
author: iainfoulds
ms.service: container-service
ms.topic: article
ms.date: 08/30/2018
ms.author: iainfou
ms.openlocfilehash: 76ad9d21f7b328e7f201d227cdd9ace51c62a3fd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857584"
---
# <a name="create-an-ingress-controller-to-an-internal-virtual-network-in-azure-kubernetes-service-aks"></a><span data-ttu-id="42448-103">Create an ingress controller to an internal virtual network in Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="42448-103">Create an ingress controller to an internal virtual network in Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="42448-104">An ingress controller is a piece of software that provides reverse proxy, configurable traffic routing, and TLS termination for Kubernetes services.</span><span class="sxs-lookup"><span data-stu-id="42448-104">An ingress controller is a piece of software that provides reverse proxy, configurable traffic routing, and TLS termination for Kubernetes services.</span></span> <span data-ttu-id="42448-105">Kubernetes ingress resources are used to configure the ingress rules and routes for individual Kubernetes services.</span><span class="sxs-lookup"><span data-stu-id="42448-105">Kubernetes ingress resources are used to configure the ingress rules and routes for individual Kubernetes services.</span></span> <span data-ttu-id="42448-106">Using an ingress controller and ingress rules, a single IP address can be used to route traffic to multiple services in a Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="42448-106">Using an ingress controller and ingress rules, a single IP address can be used to route traffic to multiple services in a Kubernetes cluster.</span></span>

<span data-ttu-id="42448-107">This article shows you how to deploy the [NGINX ingress controller][nginx-ingress] in an Azure Kubernetes Service (AKS) cluster.</span><span class="sxs-lookup"><span data-stu-id="42448-107">This article shows you how to deploy the [NGINX ingress controller][nginx-ingress] in an Azure Kubernetes Service (AKS) cluster.</span></span> <span data-ttu-id="42448-108">The ingress controller is configured on an internal, private virtual network and IP address.</span><span class="sxs-lookup"><span data-stu-id="42448-108">The ingress controller is configured on an internal, private virtual network and IP address.</span></span> <span data-ttu-id="42448-109">No external access is allowed.</span><span class="sxs-lookup"><span data-stu-id="42448-109">No external access is allowed.</span></span> <span data-ttu-id="42448-110">Two applications are then run in the AKS cluster, each of which is accessible over the single IP address.</span><span class="sxs-lookup"><span data-stu-id="42448-110">Two applications are then run in the AKS cluster, each of which is accessible over the single IP address.</span></span>

<span data-ttu-id="42448-111">You can also:</span><span class="sxs-lookup"><span data-stu-id="42448-111">You can also:</span></span>

- <span data-ttu-id="42448-112">[Create a basic ingress controller with external network connectivity][aks-ingress-basic]</span><span class="sxs-lookup"><span data-stu-id="42448-112">[Create a basic ingress controller with external network connectivity][aks-ingress-basic]</span></span>
- <span data-ttu-id="42448-113">[Enable the HTTP application routing add-on][aks-http-app-routing]</span><span class="sxs-lookup"><span data-stu-id="42448-113">[Enable the HTTP application routing add-on][aks-http-app-routing]</span></span>
- <span data-ttu-id="42448-114">[Create an ingress controller with a dynamic public IP and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-tls]</span><span class="sxs-lookup"><span data-stu-id="42448-114">[Create an ingress controller with a dynamic public IP and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-tls]</span></span>
- <span data-ttu-id="42448-115">[Create an ingress controller with a static public IP address and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-static-tls]</span><span class="sxs-lookup"><span data-stu-id="42448-115">[Create an ingress controller with a static public IP address and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-static-tls]</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="42448-116">Before you begin</span><span class="sxs-lookup"><span data-stu-id="42448-116">Before you begin</span></span>

<span data-ttu-id="42448-117">This article uses Helm to install the NGINX ingress controller, cert-manager, and a sample web app.</span><span class="sxs-lookup"><span data-stu-id="42448-117">This article uses Helm to install the NGINX ingress controller, cert-manager, and a sample web app.</span></span> <span data-ttu-id="42448-118">You need to have Helm initialized within your AKS cluster and using a service account for Tiller.</span><span class="sxs-lookup"><span data-stu-id="42448-118">You need to have Helm initialized within your AKS cluster and using a service account for Tiller.</span></span> <span data-ttu-id="42448-119">For more information on configuring and using Helm, see [Install applications with Helm in Azure Kubernetes Service (AKS)][use-helm].</span><span class="sxs-lookup"><span data-stu-id="42448-119">For more information on configuring and using Helm, see [Install applications with Helm in Azure Kubernetes Service (AKS)][use-helm].</span></span>

<span data-ttu-id="42448-120">This article also requires that you are running the Azure CLI version 2.0.41 or later.</span><span class="sxs-lookup"><span data-stu-id="42448-120">This article also requires that you are running the Azure CLI version 2.0.41 or later.</span></span> <span data-ttu-id="42448-121">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="42448-121">Run `az --version` to find the version.</span></span> <span data-ttu-id="42448-122">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span><span class="sxs-lookup"><span data-stu-id="42448-122">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span></span>

## <a name="create-an-ingress-controller"></a><span data-ttu-id="42448-123">Create an ingress controller</span><span class="sxs-lookup"><span data-stu-id="42448-123">Create an ingress controller</span></span>

<span data-ttu-id="42448-124">By default, an NGINX ingress controller is created with a dynamic public IP address assignment.</span><span class="sxs-lookup"><span data-stu-id="42448-124">By default, an NGINX ingress controller is created with a dynamic public IP address assignment.</span></span> <span data-ttu-id="42448-125">A common configuration requirement is to use an internal, private network and IP address.</span><span class="sxs-lookup"><span data-stu-id="42448-125">A common configuration requirement is to use an internal, private network and IP address.</span></span> <span data-ttu-id="42448-126">This approach allows you to restrict access to your services to internal users, with no external access.</span><span class="sxs-lookup"><span data-stu-id="42448-126">This approach allows you to restrict access to your services to internal users, with no external access.</span></span>

<span data-ttu-id="42448-127">Create a file named *internal-ingress.yaml* using the following example manifest file.</span><span class="sxs-lookup"><span data-stu-id="42448-127">Create a file named *internal-ingress.yaml* using the following example manifest file.</span></span> <span data-ttu-id="42448-128">This example assigns *10.240.0.42* to the *loadBalancerIP* resource.</span><span class="sxs-lookup"><span data-stu-id="42448-128">This example assigns *10.240.0.42* to the *loadBalancerIP* resource.</span></span> <span data-ttu-id="42448-129">Provide your own internal IP address for use with the ingress controller.</span><span class="sxs-lookup"><span data-stu-id="42448-129">Provide your own internal IP address for use with the ingress controller.</span></span> <span data-ttu-id="42448-130">Make sure that this IP address is not already in use within your virtual network.</span><span class="sxs-lookup"><span data-stu-id="42448-130">Make sure that this IP address is not already in use within your virtual network.</span></span>

```yaml
controller:
  service:
    loadBalancerIP: 10.240.0.42
    annotations:
      service.beta.kubernetes.io/azure-load-balancer-internal: "true"
```

<span data-ttu-id="42448-131">Now deploy the *nginx-ingress* chart with Helm.</span><span class="sxs-lookup"><span data-stu-id="42448-131">Now deploy the *nginx-ingress* chart with Helm.</span></span> <span data-ttu-id="42448-132">To use the manifest file created in the previous step, add the `-f internal-ingress.yaml` parameter:</span><span class="sxs-lookup"><span data-stu-id="42448-132">To use the manifest file created in the previous step, add the `-f internal-ingress.yaml` parameter:</span></span>

> [!TIP]
> <span data-ttu-id="42448-133">The following example installs the ingress controller in the `kube-system` namespace.</span><span class="sxs-lookup"><span data-stu-id="42448-133">The following example installs the ingress controller in the `kube-system` namespace.</span></span> <span data-ttu-id="42448-134">You can specify a different namespace for your own environment if desired.</span><span class="sxs-lookup"><span data-stu-id="42448-134">You can specify a different namespace for your own environment if desired.</span></span> <span data-ttu-id="42448-135">If your AKS cluster is not RBAC enabled, add `--set rbac.create=false` to the commands.</span><span class="sxs-lookup"><span data-stu-id="42448-135">If your AKS cluster is not RBAC enabled, add `--set rbac.create=false` to the commands.</span></span>

```console
helm install stable/nginx-ingress --namespace kube-system -f internal-ingress.yaml
```

<span data-ttu-id="42448-136">When the Kubernetes load balancer service is created for the NGINX ingress controller, your internal IP address is assigned, as shown in the following example output:</span><span class="sxs-lookup"><span data-stu-id="42448-136">When the Kubernetes load balancer service is created for the NGINX ingress controller, your internal IP address is assigned, as shown in the following example output:</span></span>

```
$ kubectl get service -l app=nginx-ingress --namespace kube-system

NAME                                              TYPE           CLUSTER-IP    EXTERNAL-IP   PORT(S)                      AGE
alternating-coral-nginx-ingress-controller        LoadBalancer   10.0.97.109   10.240.0.42   80:31507/TCP,443:30707/TCP   1m
alternating-coral-nginx-ingress-default-backend   ClusterIP      10.0.134.66   <none>        80/TCP                       1m
```

<span data-ttu-id="42448-137">No ingress rules have been created yet, so the NGINX ingress controller's default 404 page is displayed if you browse to the internal IP address.</span><span class="sxs-lookup"><span data-stu-id="42448-137">No ingress rules have been created yet, so the NGINX ingress controller's default 404 page is displayed if you browse to the internal IP address.</span></span> <span data-ttu-id="42448-138">Ingress rules are configured in the following steps.</span><span class="sxs-lookup"><span data-stu-id="42448-138">Ingress rules are configured in the following steps.</span></span>

## <a name="run-demo-applications"></a><span data-ttu-id="42448-139">Run demo applications</span><span class="sxs-lookup"><span data-stu-id="42448-139">Run demo applications</span></span>

<span data-ttu-id="42448-140">To see the ingress controller in action, let's run two demo applications in your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="42448-140">To see the ingress controller in action, let's run two demo applications in your AKS cluster.</span></span> <span data-ttu-id="42448-141">In this example, Helm is used to deploy two instances of a simple 'Hello world' application.</span><span class="sxs-lookup"><span data-stu-id="42448-141">In this example, Helm is used to deploy two instances of a simple 'Hello world' application.</span></span>

<span data-ttu-id="42448-142">Before you can install the sample Helm charts, add the Azure samples repository to your Helm environment as follows:</span><span class="sxs-lookup"><span data-stu-id="42448-142">Before you can install the sample Helm charts, add the Azure samples repository to your Helm environment as follows:</span></span>

```console
helm repo add azure-samples https://azure-samples.github.io/helm-charts/
```

<span data-ttu-id="42448-143">Create the first demo application from a Helm chart with the following command:</span><span class="sxs-lookup"><span data-stu-id="42448-143">Create the first demo application from a Helm chart with the following command:</span></span>

```console
helm install azure-samples/aks-helloworld
```

<span data-ttu-id="42448-144">Now install a second instance of the demo application.</span><span class="sxs-lookup"><span data-stu-id="42448-144">Now install a second instance of the demo application.</span></span> <span data-ttu-id="42448-145">For the second instance, you specify a new title so that the two applications are visually distinct.</span><span class="sxs-lookup"><span data-stu-id="42448-145">For the second instance, you specify a new title so that the two applications are visually distinct.</span></span> <span data-ttu-id="42448-146">You also specify a unique service name:</span><span class="sxs-lookup"><span data-stu-id="42448-146">You also specify a unique service name:</span></span>

```console
helm install azure-samples/aks-helloworld --set title="AKS Ingress Demo" --set serviceName="ingress-demo"
```

## <a name="create-an-ingress-route"></a><span data-ttu-id="42448-147">Create an ingress route</span><span class="sxs-lookup"><span data-stu-id="42448-147">Create an ingress route</span></span>

<span data-ttu-id="42448-148">Both applications are now running on your Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="42448-148">Both applications are now running on your Kubernetes cluster.</span></span> <span data-ttu-id="42448-149">To route traffic to each application, create a Kubernetes ingress resource.</span><span class="sxs-lookup"><span data-stu-id="42448-149">To route traffic to each application, create a Kubernetes ingress resource.</span></span> <span data-ttu-id="42448-150">The ingress resource configures the rules that route traffic to one of the two applications.</span><span class="sxs-lookup"><span data-stu-id="42448-150">The ingress resource configures the rules that route traffic to one of the two applications.</span></span>

<span data-ttu-id="42448-151">In the following example, traffic to the address `http://10.240.0.42/` is routed to the service named `aks-helloworld`.</span><span class="sxs-lookup"><span data-stu-id="42448-151">In the following example, traffic to the address `http://10.240.0.42/` is routed to the service named `aks-helloworld`.</span></span> <span data-ttu-id="42448-152">Traffic to the address `http://10.240.0.42/hello-world-two` is routed to the `ingress-demo` service.</span><span class="sxs-lookup"><span data-stu-id="42448-152">Traffic to the address `http://10.240.0.42/hello-world-two` is routed to the `ingress-demo` service.</span></span>

<span data-ttu-id="42448-153">Create a file named `hello-world-ingress.yaml` and copy in the following example YAML.</span><span class="sxs-lookup"><span data-stu-id="42448-153">Create a file named `hello-world-ingress.yaml` and copy in the following example YAML.</span></span>

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: hello-world-ingress
  annotations:
    kubernetes.io/ingress.class: nginx
    nginx.ingress.kubernetes.io/ssl-redirect: "false"
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /
        backend:
          serviceName: aks-helloworld
          servicePort: 80
      - path: /hello-world-two
        backend:
          serviceName: ingress-demo
          servicePort: 80
```

<span data-ttu-id="42448-154">Create the ingress resource using the `kubectl apply -f hello-world-ingress.yaml` command.</span><span class="sxs-lookup"><span data-stu-id="42448-154">Create the ingress resource using the `kubectl apply -f hello-world-ingress.yaml` command.</span></span>

```
$ kubectl apply -f hello-world-ingress.yaml

ingress.extensions/hello-world-ingress created
```

## <a name="test-the-ingress-controller"></a><span data-ttu-id="42448-155">Test the ingress controller</span><span class="sxs-lookup"><span data-stu-id="42448-155">Test the ingress controller</span></span>

<span data-ttu-id="42448-156">To test the routes for the ingress controller, browse to the two applications with a web client.</span><span class="sxs-lookup"><span data-stu-id="42448-156">To test the routes for the ingress controller, browse to the two applications with a web client.</span></span> <span data-ttu-id="42448-157">If needed, you can quickly test this internal-only functionality from a pod on the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="42448-157">If needed, you can quickly test this internal-only functionality from a pod on the AKS cluster.</span></span> <span data-ttu-id="42448-158">Create a test pod and attach a terminal session to it:</span><span class="sxs-lookup"><span data-stu-id="42448-158">Create a test pod and attach a terminal session to it:</span></span>

```console
kubectl run -it --rm aks-ingress-test --image=debian
```

<span data-ttu-id="42448-159">Install `curl` in the pod using `apt-get`:</span><span class="sxs-lookup"><span data-stu-id="42448-159">Install `curl` in the pod using `apt-get`:</span></span>

```console
apt-get update && apt-get install -y curl
```

<span data-ttu-id="42448-160">Now access the address of your Kubernetes ingress controller using `curl`, such as *http://10.240.0.42*.</span><span class="sxs-lookup"><span data-stu-id="42448-160">Now access the address of your Kubernetes ingress controller using `curl`, such as *http://10.240.0.42*.</span></span> <span data-ttu-id="42448-161">Provide your own internal IP address specified when you deployed the ingress controller in the first step of this article.</span><span class="sxs-lookup"><span data-stu-id="42448-161">Provide your own internal IP address specified when you deployed the ingress controller in the first step of this article.</span></span>

```console
curl -L http://10.240.0.42
```

<span data-ttu-id="42448-162">No additional path was provided with the address, so the ingress controller defaults to the */* route.</span><span class="sxs-lookup"><span data-stu-id="42448-162">No additional path was provided with the address, so the ingress controller defaults to the */* route.</span></span> <span data-ttu-id="42448-163">The first demo application is returned, as shown in the following condensed example output:</span><span class="sxs-lookup"><span data-stu-id="42448-163">The first demo application is returned, as shown in the following condensed example output:</span></span>

```
$ curl -L 10.240.0.42

<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <link rel="stylesheet" type="text/css" href="/static/default.css">
    <title>Welcome to Azure Kubernetes Service (AKS)</title>
[...]
```

<span data-ttu-id="42448-164">Now add */hello-world-two* path to the address, such as *http://10.240.0.42/hello-world-two*.</span><span class="sxs-lookup"><span data-stu-id="42448-164">Now add */hello-world-two* path to the address, such as *http://10.240.0.42/hello-world-two*.</span></span> <span data-ttu-id="42448-165">The second demo application with the custom title is returned, as shown in the following condensed example output:</span><span class="sxs-lookup"><span data-stu-id="42448-165">The second demo application with the custom title is returned, as shown in the following condensed example output:</span></span>

```
$ curl -L -k http://10.240.0.42/hello-world-two

<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <link rel="stylesheet" type="text/css" href="/static/default.css">
    <title>AKS Ingress Demo</title>
[...]
```

## <a name="next-steps"></a><span data-ttu-id="42448-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="42448-166">Next steps</span></span>

<span data-ttu-id="42448-167">This article included some external components to AKS.</span><span class="sxs-lookup"><span data-stu-id="42448-167">This article included some external components to AKS.</span></span> <span data-ttu-id="42448-168">To learn more about these components, see the following project pages:</span><span class="sxs-lookup"><span data-stu-id="42448-168">To learn more about these components, see the following project pages:</span></span>

- <span data-ttu-id="42448-169">[Helm CLI][helm-cli]</span><span class="sxs-lookup"><span data-stu-id="42448-169">[Helm CLI][helm-cli]</span></span>
- <span data-ttu-id="42448-170">[NGINX ingress controller][nginx-ingress]</span><span class="sxs-lookup"><span data-stu-id="42448-170">[NGINX ingress controller][nginx-ingress]</span></span>

<span data-ttu-id="42448-171">You can also:</span><span class="sxs-lookup"><span data-stu-id="42448-171">You can also:</span></span>

- <span data-ttu-id="42448-172">[Create a basic ingress controller with external network connectivity][aks-ingress-basic]</span><span class="sxs-lookup"><span data-stu-id="42448-172">[Create a basic ingress controller with external network connectivity][aks-ingress-basic]</span></span>
- <span data-ttu-id="42448-173">[Enable the HTTP application routing add-on][aks-http-app-routing]</span><span class="sxs-lookup"><span data-stu-id="42448-173">[Enable the HTTP application routing add-on][aks-http-app-routing]</span></span>
- <span data-ttu-id="42448-174">[Create an ingress controller with a dynamic public IP and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-tls]</span><span class="sxs-lookup"><span data-stu-id="42448-174">[Create an ingress controller with a dynamic public IP and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-tls]</span></span>
- <span data-ttu-id="42448-175">[Create an ingress controller with a static public IP address and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-static-tls]</span><span class="sxs-lookup"><span data-stu-id="42448-175">[Create an ingress controller with a static public IP address and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-static-tls]</span></span>

<!-- LINKS - external -->
[helm-cli]: https://docs.microsoft.com/azure/aks/kubernetes-helm#install-helm-cli
[nginx-ingress]: https://github.com/kubernetes/ingress-nginx

<!-- LINKS - internal -->
[use-helm]: kubernetes-helm.md
[azure-cli-install]: /cli/azure/install-azure-cli
[aks-ingress-basic]: ingress-basic.md
[aks-ingress-tls]: ingress-tls.md
[aks-ingress-static-tls]: ingress-static-ip.md
[aks-http-app-routing]: http-application-routing.md
