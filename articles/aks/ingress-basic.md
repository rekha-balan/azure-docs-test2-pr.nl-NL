---
title: Create a basic ingress controller in Azure Kubernetes Service (AKS)
description: Learn how to install and configure a basic NGINX ingress controller in an Azure Kubernetes Service (AKS) cluster.
services: container-service
author: iainfoulds
ms.service: container-service
ms.topic: article
ms.date: 08/30/2018
ms.author: iainfou
ms.openlocfilehash: 3ae7a3193e0a4bacc64524f477b6c179ead20b6b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866174"
---
# <a name="create-an-ingress-controller-in-azure-kubernetes-service-aks"></a><span data-ttu-id="57367-103">Create an ingress controller in Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="57367-103">Create an ingress controller in Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="57367-104">An ingress controller is a piece of software that provides reverse proxy, configurable traffic routing, and TLS termination for Kubernetes services.</span><span class="sxs-lookup"><span data-stu-id="57367-104">An ingress controller is a piece of software that provides reverse proxy, configurable traffic routing, and TLS termination for Kubernetes services.</span></span> <span data-ttu-id="57367-105">Kubernetes ingress resources are used to configure the ingress rules and routes for individual Kubernetes services.</span><span class="sxs-lookup"><span data-stu-id="57367-105">Kubernetes ingress resources are used to configure the ingress rules and routes for individual Kubernetes services.</span></span> <span data-ttu-id="57367-106">Using an ingress controller and ingress rules, a single IP address can be used to route traffic to multiple services in a Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="57367-106">Using an ingress controller and ingress rules, a single IP address can be used to route traffic to multiple services in a Kubernetes cluster.</span></span>

<span data-ttu-id="57367-107">This article shows you how to deploy the [NGINX ingress controller][nginx-ingress] in an Azure Kubernetes Service (AKS) cluster.</span><span class="sxs-lookup"><span data-stu-id="57367-107">This article shows you how to deploy the [NGINX ingress controller][nginx-ingress] in an Azure Kubernetes Service (AKS) cluster.</span></span> <span data-ttu-id="57367-108">Two applications are then run in the AKS cluster, each of which is accessible over the single IP address.</span><span class="sxs-lookup"><span data-stu-id="57367-108">Two applications are then run in the AKS cluster, each of which is accessible over the single IP address.</span></span>

<span data-ttu-id="57367-109">You can also:</span><span class="sxs-lookup"><span data-stu-id="57367-109">You can also:</span></span>

- <span data-ttu-id="57367-110">[Enable the HTTP application routing add-on][aks-http-app-routing]</span><span class="sxs-lookup"><span data-stu-id="57367-110">[Enable the HTTP application routing add-on][aks-http-app-routing]</span></span>
- <span data-ttu-id="57367-111">[Create an ingress controller that uses an internal, private network and IP address][aks-ingress-internal]</span><span class="sxs-lookup"><span data-stu-id="57367-111">[Create an ingress controller that uses an internal, private network and IP address][aks-ingress-internal]</span></span>
- <span data-ttu-id="57367-112">[Create an ingress controller with a dynamic public IP and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-tls]</span><span class="sxs-lookup"><span data-stu-id="57367-112">[Create an ingress controller with a dynamic public IP and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-tls]</span></span>
- <span data-ttu-id="57367-113">[Create an ingress controller with a static public IP address and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-static-tls]</span><span class="sxs-lookup"><span data-stu-id="57367-113">[Create an ingress controller with a static public IP address and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-static-tls]</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="57367-114">Before you begin</span><span class="sxs-lookup"><span data-stu-id="57367-114">Before you begin</span></span>

<span data-ttu-id="57367-115">This article uses Helm to install the NGINX ingress controller, cert-manager, and a sample web app.</span><span class="sxs-lookup"><span data-stu-id="57367-115">This article uses Helm to install the NGINX ingress controller, cert-manager, and a sample web app.</span></span> <span data-ttu-id="57367-116">You need to have Helm initialized within your AKS cluster and using a service account for Tiller.</span><span class="sxs-lookup"><span data-stu-id="57367-116">You need to have Helm initialized within your AKS cluster and using a service account for Tiller.</span></span> <span data-ttu-id="57367-117">For more information on configuring and using Helm, see [Install applications with Helm in Azure Kubernetes Service (AKS)][use-helm].</span><span class="sxs-lookup"><span data-stu-id="57367-117">For more information on configuring and using Helm, see [Install applications with Helm in Azure Kubernetes Service (AKS)][use-helm].</span></span>

<span data-ttu-id="57367-118">This article also requires that you are running the Azure CLI version 2.0.41 or later.</span><span class="sxs-lookup"><span data-stu-id="57367-118">This article also requires that you are running the Azure CLI version 2.0.41 or later.</span></span> <span data-ttu-id="57367-119">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="57367-119">Run `az --version` to find the version.</span></span> <span data-ttu-id="57367-120">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span><span class="sxs-lookup"><span data-stu-id="57367-120">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span></span>

## <a name="create-an-ingress-controller"></a><span data-ttu-id="57367-121">Create an ingress controller</span><span class="sxs-lookup"><span data-stu-id="57367-121">Create an ingress controller</span></span>

<span data-ttu-id="57367-122">To create the ingress controller, use `Helm` to install *nginx-ingress*.</span><span class="sxs-lookup"><span data-stu-id="57367-122">To create the ingress controller, use `Helm` to install *nginx-ingress*.</span></span>

> [!TIP]
> <span data-ttu-id="57367-123">The following example installs the ingress controller in the `kube-system` namespace.</span><span class="sxs-lookup"><span data-stu-id="57367-123">The following example installs the ingress controller in the `kube-system` namespace.</span></span> <span data-ttu-id="57367-124">You can specify a different namespace for your own environment if desired.</span><span class="sxs-lookup"><span data-stu-id="57367-124">You can specify a different namespace for your own environment if desired.</span></span> <span data-ttu-id="57367-125">If your AKS cluster is not RBAC enabled, add `--set rbac.create=false` to the commands.</span><span class="sxs-lookup"><span data-stu-id="57367-125">If your AKS cluster is not RBAC enabled, add `--set rbac.create=false` to the commands.</span></span>

```console
helm install stable/nginx-ingress --namespace kube-system
```

<span data-ttu-id="57367-126">When the Kubernetes load balancer service is created for the NGINX ingress controller, a dynamic public IP address is assigned, as shown in the following example output:</span><span class="sxs-lookup"><span data-stu-id="57367-126">When the Kubernetes load balancer service is created for the NGINX ingress controller, a dynamic public IP address is assigned, as shown in the following example output:</span></span>

```
$ kubectl get service -l app=nginx-ingress --namespace kube-system

NAME                                         TYPE           CLUSTER-IP    EXTERNAL-IP   PORT(S)                      AGE
masked-otter-nginx-ingress-controller        LoadBalancer   10.0.92.99    40.117.74.8   80:31077/TCP,443:32592/TCP   7m
masked-otter-nginx-ingress-default-backend   ClusterIP      10.0.46.106   <none>        80/TCP                       7m
```

<span data-ttu-id="57367-127">No ingress rules have been created yet, so the NGINX ingress controller's default 404 page is displayed if you browse to the internal IP address.</span><span class="sxs-lookup"><span data-stu-id="57367-127">No ingress rules have been created yet, so the NGINX ingress controller's default 404 page is displayed if you browse to the internal IP address.</span></span> <span data-ttu-id="57367-128">Ingress rules are configured in the following steps.</span><span class="sxs-lookup"><span data-stu-id="57367-128">Ingress rules are configured in the following steps.</span></span>

## <a name="run-demo-applications"></a><span data-ttu-id="57367-129">Run demo applications</span><span class="sxs-lookup"><span data-stu-id="57367-129">Run demo applications</span></span>

<span data-ttu-id="57367-130">To see the ingress controller in action, let's run two demo applications in your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="57367-130">To see the ingress controller in action, let's run two demo applications in your AKS cluster.</span></span> <span data-ttu-id="57367-131">In this example, Helm is used to deploy two instances of a simple 'Hello world' application.</span><span class="sxs-lookup"><span data-stu-id="57367-131">In this example, Helm is used to deploy two instances of a simple 'Hello world' application.</span></span>

<span data-ttu-id="57367-132">Before you can install the sample Helm charts, add the Azure samples repository to your Helm environment as follows:</span><span class="sxs-lookup"><span data-stu-id="57367-132">Before you can install the sample Helm charts, add the Azure samples repository to your Helm environment as follows:</span></span>

```console
helm repo add azure-samples https://azure-samples.github.io/helm-charts/
```

<span data-ttu-id="57367-133">Create the first demo application from a Helm chart with the following command:</span><span class="sxs-lookup"><span data-stu-id="57367-133">Create the first demo application from a Helm chart with the following command:</span></span>

```console
helm install azure-samples/aks-helloworld
```

<span data-ttu-id="57367-134">Now install a second instance of the demo application.</span><span class="sxs-lookup"><span data-stu-id="57367-134">Now install a second instance of the demo application.</span></span> <span data-ttu-id="57367-135">For the second instance, you specify a new title so that the two applications are visually distinct.</span><span class="sxs-lookup"><span data-stu-id="57367-135">For the second instance, you specify a new title so that the two applications are visually distinct.</span></span> <span data-ttu-id="57367-136">You also specify a unique service name:</span><span class="sxs-lookup"><span data-stu-id="57367-136">You also specify a unique service name:</span></span>

```console
helm install azure-samples/aks-helloworld --set title="AKS Ingress Demo" --set serviceName="ingress-demo"
```

## <a name="create-an-ingress-route"></a><span data-ttu-id="57367-137">Create an ingress route</span><span class="sxs-lookup"><span data-stu-id="57367-137">Create an ingress route</span></span>

<span data-ttu-id="57367-138">Both applications are now running on your Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="57367-138">Both applications are now running on your Kubernetes cluster.</span></span> <span data-ttu-id="57367-139">To route traffic to each application, create a Kubernetes ingress resource.</span><span class="sxs-lookup"><span data-stu-id="57367-139">To route traffic to each application, create a Kubernetes ingress resource.</span></span> <span data-ttu-id="57367-140">The ingress resource configures the rules that route traffic to one of the two applications.</span><span class="sxs-lookup"><span data-stu-id="57367-140">The ingress resource configures the rules that route traffic to one of the two applications.</span></span>

<span data-ttu-id="57367-141">In the following example, traffic to the address `http://40.117.74.8/` is routed to the service named `aks-helloworld`.</span><span class="sxs-lookup"><span data-stu-id="57367-141">In the following example, traffic to the address `http://40.117.74.8/` is routed to the service named `aks-helloworld`.</span></span> <span data-ttu-id="57367-142">Traffic to the address `http://40.117.74.8/hello-world-two` is routed to the `ingress-demo` service.</span><span class="sxs-lookup"><span data-stu-id="57367-142">Traffic to the address `http://40.117.74.8/hello-world-two` is routed to the `ingress-demo` service.</span></span>

<span data-ttu-id="57367-143">Create a file named `hello-world-ingress.yaml` and copy in the following example YAML.</span><span class="sxs-lookup"><span data-stu-id="57367-143">Create a file named `hello-world-ingress.yaml` and copy in the following example YAML.</span></span>

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

<span data-ttu-id="57367-144">Create the ingress resource using the `kubectl apply -f hello-world-ingress.yaml` command.</span><span class="sxs-lookup"><span data-stu-id="57367-144">Create the ingress resource using the `kubectl apply -f hello-world-ingress.yaml` command.</span></span>

```
$ kubectl apply -f hello-world-ingress.yaml

ingress.extensions/hello-world-ingress created
```

## <a name="test-the-ingress-controller"></a><span data-ttu-id="57367-145">Test the ingress controller</span><span class="sxs-lookup"><span data-stu-id="57367-145">Test the ingress controller</span></span>

<span data-ttu-id="57367-146">To test the routes for the ingress controller, browse to the two applications.</span><span class="sxs-lookup"><span data-stu-id="57367-146">To test the routes for the ingress controller, browse to the two applications.</span></span> <span data-ttu-id="57367-147">Open a web browser to the IP address of your NGINX ingress controller, such as *http://40.117.74.8*.</span><span class="sxs-lookup"><span data-stu-id="57367-147">Open a web browser to the IP address of your NGINX ingress controller, such as *http://40.117.74.8*.</span></span> <span data-ttu-id="57367-148">The first demo application is displayed in the web browser, as shown in the follow example:</span><span class="sxs-lookup"><span data-stu-id="57367-148">The first demo application is displayed in the web browser, as shown in the follow example:</span></span>

![First app running behind the ingress controller](media/ingress-basic/app-one.png)

<span data-ttu-id="57367-150">Now add the */hello-world-two* path to the IP address, such as *http://40.117.74.8/hello-world-two*.</span><span class="sxs-lookup"><span data-stu-id="57367-150">Now add the */hello-world-two* path to the IP address, such as *http://40.117.74.8/hello-world-two*.</span></span> <span data-ttu-id="57367-151">The second demo application with the custom title is displayed:</span><span class="sxs-lookup"><span data-stu-id="57367-151">The second demo application with the custom title is displayed:</span></span>

![Second app running behind the ingress controller](media/ingress-basic/app-two.png)

## <a name="next-steps"></a><span data-ttu-id="57367-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="57367-153">Next steps</span></span>

<span data-ttu-id="57367-154">This article included some external components to AKS.</span><span class="sxs-lookup"><span data-stu-id="57367-154">This article included some external components to AKS.</span></span> <span data-ttu-id="57367-155">To learn more about these components, see the following project pages:</span><span class="sxs-lookup"><span data-stu-id="57367-155">To learn more about these components, see the following project pages:</span></span>

- <span data-ttu-id="57367-156">[Helm CLI][helm-cli]</span><span class="sxs-lookup"><span data-stu-id="57367-156">[Helm CLI][helm-cli]</span></span>
- <span data-ttu-id="57367-157">[NGINX ingress controller][nginx-ingress]</span><span class="sxs-lookup"><span data-stu-id="57367-157">[NGINX ingress controller][nginx-ingress]</span></span>

<span data-ttu-id="57367-158">You can also:</span><span class="sxs-lookup"><span data-stu-id="57367-158">You can also:</span></span>

- <span data-ttu-id="57367-159">[Enable the HTTP application routing add-on][aks-http-app-routing]</span><span class="sxs-lookup"><span data-stu-id="57367-159">[Enable the HTTP application routing add-on][aks-http-app-routing]</span></span>
- <span data-ttu-id="57367-160">[Create an ingress controller that uses an internal, private network and IP address][aks-ingress-internal]</span><span class="sxs-lookup"><span data-stu-id="57367-160">[Create an ingress controller that uses an internal, private network and IP address][aks-ingress-internal]</span></span>
- <span data-ttu-id="57367-161">[Create an ingress controller with a dynamic public IP and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-tls]</span><span class="sxs-lookup"><span data-stu-id="57367-161">[Create an ingress controller with a dynamic public IP and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-tls]</span></span>
- <span data-ttu-id="57367-162">[Create an ingress controller with a static public IP address and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-static-tls]</span><span class="sxs-lookup"><span data-stu-id="57367-162">[Create an ingress controller with a static public IP address and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-static-tls]</span></span>

<!-- LINKS - external -->
[helm-cli]: https://docs.microsoft.com/azure/aks/kubernetes-helm#install-helm-cli
[nginx-ingress]: https://github.com/kubernetes/ingress-nginx

<!-- LINKS - internal -->
[use-helm]: kubernetes-helm.md
[azure-cli-install]: /cli/azure/install-azure-cli
[aks-ingress-internal]: ingress-internal-ip.md
[aks-ingress-tls]: ingress-tls.md
[aks-ingress-static-tls]: ingress-static-ip.md
[aks-http-app-routing]: http-application-routing.md
