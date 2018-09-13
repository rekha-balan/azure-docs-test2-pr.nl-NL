---
title: Create an HTTPS ingress with Azure Kubernetes Service (AKS) cluster
description: Learn how to install and configure an NGINX ingress controller that uses Let's Encrypt for automatic SSL certificate generation in an Azure Kubernetes Service (AKS) cluster.
services: container-service
author: iainfoulds
ms.service: container-service
ms.topic: article
ms.date: 08/30/2018
ms.author: iainfou
ms.openlocfilehash: 87ea88ad84114c4059e9a461beedb656c1d66bf5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867030"
---
# <a name="create-an-https-ingress-controller-on-azure-kubernetes-service-aks"></a><span data-ttu-id="3b04d-103">Create an HTTPS ingress controller on Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="3b04d-103">Create an HTTPS ingress controller on Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="3b04d-104">An ingress controller is a piece of software that provides reverse proxy, configurable traffic routing, and TLS termination for Kubernetes services.</span><span class="sxs-lookup"><span data-stu-id="3b04d-104">An ingress controller is a piece of software that provides reverse proxy, configurable traffic routing, and TLS termination for Kubernetes services.</span></span> <span data-ttu-id="3b04d-105">Kubernetes ingress resources are used to configure the ingress rules and routes for individual Kubernetes services.</span><span class="sxs-lookup"><span data-stu-id="3b04d-105">Kubernetes ingress resources are used to configure the ingress rules and routes for individual Kubernetes services.</span></span> <span data-ttu-id="3b04d-106">Using an ingress controller and ingress rules, a single IP address can be used to route traffic to multiple services in a Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="3b04d-106">Using an ingress controller and ingress rules, a single IP address can be used to route traffic to multiple services in a Kubernetes cluster.</span></span>

<span data-ttu-id="3b04d-107">This article shows you how to deploy the [NGINX ingress controller][nginx-ingress] in an Azure Kubernetes Service (AKS) cluster.</span><span class="sxs-lookup"><span data-stu-id="3b04d-107">This article shows you how to deploy the [NGINX ingress controller][nginx-ingress] in an Azure Kubernetes Service (AKS) cluster.</span></span> <span data-ttu-id="3b04d-108">The [cert-manager][cert-manager] project is used to automatically generate and configure [Let's Encrypt][lets-encrypt] certificates.</span><span class="sxs-lookup"><span data-stu-id="3b04d-108">The [cert-manager][cert-manager] project is used to automatically generate and configure [Let's Encrypt][lets-encrypt] certificates.</span></span> <span data-ttu-id="3b04d-109">Finally, two applications are run in the AKS cluster, each of which is accessible over a single IP address.</span><span class="sxs-lookup"><span data-stu-id="3b04d-109">Finally, two applications are run in the AKS cluster, each of which is accessible over a single IP address.</span></span>

<span data-ttu-id="3b04d-110">You can also:</span><span class="sxs-lookup"><span data-stu-id="3b04d-110">You can also:</span></span>

- <span data-ttu-id="3b04d-111">[Create a basic ingress controller with external network connectivity][aks-ingress-basic]</span><span class="sxs-lookup"><span data-stu-id="3b04d-111">[Create a basic ingress controller with external network connectivity][aks-ingress-basic]</span></span>
- <span data-ttu-id="3b04d-112">[Enable the HTTP application routing add-on][aks-http-app-routing]</span><span class="sxs-lookup"><span data-stu-id="3b04d-112">[Enable the HTTP application routing add-on][aks-http-app-routing]</span></span>
- <span data-ttu-id="3b04d-113">[Create an ingress controller that uses an internal, private network and IP address][aks-ingress-internal]</span><span class="sxs-lookup"><span data-stu-id="3b04d-113">[Create an ingress controller that uses an internal, private network and IP address][aks-ingress-internal]</span></span>
- <span data-ttu-id="3b04d-114">[Create an ingress controller with a static public IP address and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-static-tls]</span><span class="sxs-lookup"><span data-stu-id="3b04d-114">[Create an ingress controller with a static public IP address and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-static-tls]</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3b04d-115">Before you begin</span><span class="sxs-lookup"><span data-stu-id="3b04d-115">Before you begin</span></span>

<span data-ttu-id="3b04d-116">This article uses Helm to install the NGINX ingress controller, cert-manager, and a sample web app.</span><span class="sxs-lookup"><span data-stu-id="3b04d-116">This article uses Helm to install the NGINX ingress controller, cert-manager, and a sample web app.</span></span> <span data-ttu-id="3b04d-117">You need to have Helm initialized within your AKS cluster and using a service account for Tiller.</span><span class="sxs-lookup"><span data-stu-id="3b04d-117">You need to have Helm initialized within your AKS cluster and using a service account for Tiller.</span></span> <span data-ttu-id="3b04d-118">Make sure that you are using the latest release of Helm.</span><span class="sxs-lookup"><span data-stu-id="3b04d-118">Make sure that you are using the latest release of Helm.</span></span> <span data-ttu-id="3b04d-119">For upgrade instructions, see the [Helm install docs][helm-install]. For more information on configuring and using Helm, see [Install applications with Helm in Azure Kubernetes Service (AKS)][use-helm].</span><span class="sxs-lookup"><span data-stu-id="3b04d-119">For upgrade instructions, see the [Helm install docs][helm-install]. For more information on configuring and using Helm, see [Install applications with Helm in Azure Kubernetes Service (AKS)][use-helm].</span></span>

<span data-ttu-id="3b04d-120">This article also requires that you are running the Azure CLI version 2.0.41 or later.</span><span class="sxs-lookup"><span data-stu-id="3b04d-120">This article also requires that you are running the Azure CLI version 2.0.41 or later.</span></span> <span data-ttu-id="3b04d-121">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="3b04d-121">Run `az --version` to find the version.</span></span> <span data-ttu-id="3b04d-122">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span><span class="sxs-lookup"><span data-stu-id="3b04d-122">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span></span>

## <a name="create-an-ingress-controller"></a><span data-ttu-id="3b04d-123">Create an ingress controller</span><span class="sxs-lookup"><span data-stu-id="3b04d-123">Create an ingress controller</span></span>

<span data-ttu-id="3b04d-124">To create the ingress controller, use `Helm` to install *nginx-ingress*.</span><span class="sxs-lookup"><span data-stu-id="3b04d-124">To create the ingress controller, use `Helm` to install *nginx-ingress*.</span></span>

> [!TIP]
> <span data-ttu-id="3b04d-125">The following example installs the ingress controller in the `kube-system` namespace.</span><span class="sxs-lookup"><span data-stu-id="3b04d-125">The following example installs the ingress controller in the `kube-system` namespace.</span></span> <span data-ttu-id="3b04d-126">You can specify a different namespace for your own environment if desired.</span><span class="sxs-lookup"><span data-stu-id="3b04d-126">You can specify a different namespace for your own environment if desired.</span></span> <span data-ttu-id="3b04d-127">If your AKS cluster is not RBAC enabled, add `--set rbac.create=false` to the commands.</span><span class="sxs-lookup"><span data-stu-id="3b04d-127">If your AKS cluster is not RBAC enabled, add `--set rbac.create=false` to the commands.</span></span>

```console
helm install stable/nginx-ingress --namespace kube-system
```

<span data-ttu-id="3b04d-128">During the installation, an Azure public IP address is created for the ingress controller.</span><span class="sxs-lookup"><span data-stu-id="3b04d-128">During the installation, an Azure public IP address is created for the ingress controller.</span></span> <span data-ttu-id="3b04d-129">This public IP address is static for the life-span of the ingress controller.</span><span class="sxs-lookup"><span data-stu-id="3b04d-129">This public IP address is static for the life-span of the ingress controller.</span></span> <span data-ttu-id="3b04d-130">If you delete the ingress controller, the public IP address assignment is lost.</span><span class="sxs-lookup"><span data-stu-id="3b04d-130">If you delete the ingress controller, the public IP address assignment is lost.</span></span> <span data-ttu-id="3b04d-131">If you then create an additional ingress controller, a new public IP address is assigned.</span><span class="sxs-lookup"><span data-stu-id="3b04d-131">If you then create an additional ingress controller, a new public IP address is assigned.</span></span> <span data-ttu-id="3b04d-132">If you wish to retain the use of the public IP address, you can instead [create an ingress controller with a static public IP address][aks-ingress-static-tls].</span><span class="sxs-lookup"><span data-stu-id="3b04d-132">If you wish to retain the use of the public IP address, you can instead [create an ingress controller with a static public IP address][aks-ingress-static-tls].</span></span>

<span data-ttu-id="3b04d-133">To get the public IP address, use the `kubectl get service` command.</span><span class="sxs-lookup"><span data-stu-id="3b04d-133">To get the public IP address, use the `kubectl get service` command.</span></span> <span data-ttu-id="3b04d-134">It takes a few minutes for the IP address to be assigned to the service.</span><span class="sxs-lookup"><span data-stu-id="3b04d-134">It takes a few minutes for the IP address to be assigned to the service.</span></span>

```
$ kubectl get service -l app=nginx-ingress --namespace kube-system

NAME                                       TYPE           CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
eager-crab-nginx-ingress-controller        LoadBalancer   10.0.182.160   51.145.155.210  80:30920/TCP,443:30426/TCP   20m
eager-crab-nginx-ingress-default-backend   ClusterIP      10.0.255.77    <none>          80/TCP                       20m
```

<span data-ttu-id="3b04d-135">No ingress rules have been created yet.</span><span class="sxs-lookup"><span data-stu-id="3b04d-135">No ingress rules have been created yet.</span></span> <span data-ttu-id="3b04d-136">If you browse to the public IP address, the NGINX ingress controller's default 404 page is displayed.</span><span class="sxs-lookup"><span data-stu-id="3b04d-136">If you browse to the public IP address, the NGINX ingress controller's default 404 page is displayed.</span></span>

## <a name="configure-a-dns-name"></a><span data-ttu-id="3b04d-137">Configure a DNS name</span><span class="sxs-lookup"><span data-stu-id="3b04d-137">Configure a DNS name</span></span>

<span data-ttu-id="3b04d-138">For the HTTPS certificates to work correctly, configure an FQDN for the ingress controller IP address.</span><span class="sxs-lookup"><span data-stu-id="3b04d-138">For the HTTPS certificates to work correctly, configure an FQDN for the ingress controller IP address.</span></span> <span data-ttu-id="3b04d-139">Update the following script with the IP address of your ingress controller and a unique name that you would like to use for the FQDN:</span><span class="sxs-lookup"><span data-stu-id="3b04d-139">Update the following script with the IP address of your ingress controller and a unique name that you would like to use for the FQDN:</span></span>

```console
#!/bin/bash

# Public IP address of your ingress controller
IP="51.145.155.210"

# Name to associate with public IP address
DNSNAME="demo-aks-ingress"

# Get the resource-id of the public ip
PUBLICIPID=$(az network public-ip list --query "[?ipAddress!=null]|[?contains(ipAddress, '$IP')].[id]" --output tsv)

# Update public ip address with DNS name
az network public-ip update --ids $PUBLICIPID --dns-name $DNSNAME
```

<span data-ttu-id="3b04d-140">The ingress controller is now accessible through the FQDN.</span><span class="sxs-lookup"><span data-stu-id="3b04d-140">The ingress controller is now accessible through the FQDN.</span></span>

## <a name="install-cert-manager"></a><span data-ttu-id="3b04d-141">Install cert-manager</span><span class="sxs-lookup"><span data-stu-id="3b04d-141">Install cert-manager</span></span>

<span data-ttu-id="3b04d-142">The NGINX ingress controller supports TLS termination.</span><span class="sxs-lookup"><span data-stu-id="3b04d-142">The NGINX ingress controller supports TLS termination.</span></span> <span data-ttu-id="3b04d-143">There are several ways to retrieve and configure certificates for HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3b04d-143">There are several ways to retrieve and configure certificates for HTTPS.</span></span> <span data-ttu-id="3b04d-144">This article demonstrates using [cert-manager][cert-manager], which provides automatic [Lets Encrypt][lets-encrypt] certificate generation and management functionality.</span><span class="sxs-lookup"><span data-stu-id="3b04d-144">This article demonstrates using [cert-manager][cert-manager], which provides automatic [Lets Encrypt][lets-encrypt] certificate generation and management functionality.</span></span>

> [!NOTE]
> <span data-ttu-id="3b04d-145">This article uses the `staging` environment for Let's Encrypt.</span><span class="sxs-lookup"><span data-stu-id="3b04d-145">This article uses the `staging` environment for Let's Encrypt.</span></span> <span data-ttu-id="3b04d-146">In production deployments, use `letsencrypt-prod` and `https://acme-v02.api.letsencrypt.org/directory` in the resource definitions and when installing the Helm chart.</span><span class="sxs-lookup"><span data-stu-id="3b04d-146">In production deployments, use `letsencrypt-prod` and `https://acme-v02.api.letsencrypt.org/directory` in the resource definitions and when installing the Helm chart.</span></span>

<span data-ttu-id="3b04d-147">To install the cert-manager controller in an RBAC-enabled cluster, use the following `helm install` command:</span><span class="sxs-lookup"><span data-stu-id="3b04d-147">To install the cert-manager controller in an RBAC-enabled cluster, use the following `helm install` command:</span></span>

```console
helm install stable/cert-manager --set ingressShim.defaultIssuerName=letsencrypt-staging --set ingressShim.defaultIssuerKind=ClusterIssuer
```

<span data-ttu-id="3b04d-148">If your cluster is not RBAC enabled, instead use the following command:</span><span class="sxs-lookup"><span data-stu-id="3b04d-148">If your cluster is not RBAC enabled, instead use the following command:</span></span>

```console
helm install stable/cert-manager \
  --set ingressShim.defaultIssuerName=letsencrypt-staging \
  --set ingressShim.defaultIssuerKind=ClusterIssuer \
  --set rbac.create=false \
  --set serviceAccount.create=false
```

<span data-ttu-id="3b04d-149">For more information on cert-manager configuration, see the [cert-manager project][cert-manager].</span><span class="sxs-lookup"><span data-stu-id="3b04d-149">For more information on cert-manager configuration, see the [cert-manager project][cert-manager].</span></span>

## <a name="create-a-ca-cluster-issuer"></a><span data-ttu-id="3b04d-150">Create a CA cluster issuer</span><span class="sxs-lookup"><span data-stu-id="3b04d-150">Create a CA cluster issuer</span></span>

<span data-ttu-id="3b04d-151">Before certificates can be issued, cert-manager requires an [Issuer][cert-manager-issuer] or [ClusterIssuer][cert-manager-cluster-issuer] resource.</span><span class="sxs-lookup"><span data-stu-id="3b04d-151">Before certificates can be issued, cert-manager requires an [Issuer][cert-manager-issuer] or [ClusterIssuer][cert-manager-cluster-issuer] resource.</span></span> <span data-ttu-id="3b04d-152">These Kubernetes resources are identical in functionality, however `Issuer` works in a single namespace, and `ClusterIssuer` works across all namespaces.</span><span class="sxs-lookup"><span data-stu-id="3b04d-152">These Kubernetes resources are identical in functionality, however `Issuer` works in a single namespace, and `ClusterIssuer` works across all namespaces.</span></span> <span data-ttu-id="3b04d-153">For more information, see the [cert-manager issuer][cert-manager-issuer] documentation.</span><span class="sxs-lookup"><span data-stu-id="3b04d-153">For more information, see the [cert-manager issuer][cert-manager-issuer] documentation.</span></span>

<span data-ttu-id="3b04d-154">Create a cluster issuer, such as `cluster-issuer.yaml`, using the following example manifest.</span><span class="sxs-lookup"><span data-stu-id="3b04d-154">Create a cluster issuer, such as `cluster-issuer.yaml`, using the following example manifest.</span></span> <span data-ttu-id="3b04d-155">Update the email address with a valid address from your organization:</span><span class="sxs-lookup"><span data-stu-id="3b04d-155">Update the email address with a valid address from your organization:</span></span>

```yaml
apiVersion: certmanager.k8s.io/v1alpha1
kind: ClusterIssuer
metadata:
  name: letsencrypt-staging
spec:
  acme:
    server: https://acme-staging-v02.api.letsencrypt.org/directory
    email: user@contoso.com
    privateKeySecretRef:
      name: letsencrypt-staging
    http01: {}
```

<span data-ttu-id="3b04d-156">To create the issuer, use the `kubectl apply -f cluster-issuer.yaml` command.</span><span class="sxs-lookup"><span data-stu-id="3b04d-156">To create the issuer, use the `kubectl apply -f cluster-issuer.yaml` command.</span></span>

```
$ kubectl apply -f cluster-issuer.yaml

clusterissuer.certmanager.k8s.io/letsencrypt-staging created
```

## <a name="create-a-certificate-object"></a><span data-ttu-id="3b04d-157">Create a certificate object</span><span class="sxs-lookup"><span data-stu-id="3b04d-157">Create a certificate object</span></span>

<span data-ttu-id="3b04d-158">Next, a certificate resource must be created.</span><span class="sxs-lookup"><span data-stu-id="3b04d-158">Next, a certificate resource must be created.</span></span> <span data-ttu-id="3b04d-159">The certificate resource defines the desired X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="3b04d-159">The certificate resource defines the desired X.509 certificate.</span></span> <span data-ttu-id="3b04d-160">For more information, see [cert-manager certificates][cert-manager-certificates].</span><span class="sxs-lookup"><span data-stu-id="3b04d-160">For more information, see [cert-manager certificates][cert-manager-certificates].</span></span>

<span data-ttu-id="3b04d-161">Create the certificate resource, such as `certificates.yaml`, with the following example manifest.</span><span class="sxs-lookup"><span data-stu-id="3b04d-161">Create the certificate resource, such as `certificates.yaml`, with the following example manifest.</span></span> <span data-ttu-id="3b04d-162">Update the *dnsNames* and *domains* to the DNS name you created in a previous step.</span><span class="sxs-lookup"><span data-stu-id="3b04d-162">Update the *dnsNames* and *domains* to the DNS name you created in a previous step.</span></span> <span data-ttu-id="3b04d-163">If you use an internal-only ingress controller, specify the internal DNS name for your service.</span><span class="sxs-lookup"><span data-stu-id="3b04d-163">If you use an internal-only ingress controller, specify the internal DNS name for your service.</span></span>

```yaml
apiVersion: certmanager.k8s.io/v1alpha1
kind: Certificate
metadata:
  name: tls-secret
spec:
  secretName: tls-secret
  dnsNames:
  - demo-aks-ingress.eastus.cloudapp.azure.com
  acme:
    config:
    - http01:
        ingressClass: nginx
      domains:
      - demo-aks-ingress.eastus.cloudapp.azure.com
  issuerRef:
    name: letsencrypt-staging
    kind: ClusterIssuer
```

<span data-ttu-id="3b04d-164">To create the certificate resource, use the `kubectl apply -f certificates.yaml` command.</span><span class="sxs-lookup"><span data-stu-id="3b04d-164">To create the certificate resource, use the `kubectl apply -f certificates.yaml` command.</span></span>

```
$ kubectl apply -f certificates.yaml

certificate.certmanager.k8s.io/tls-secret created
```

## <a name="run-demo-applications"></a><span data-ttu-id="3b04d-165">Run demo applications</span><span class="sxs-lookup"><span data-stu-id="3b04d-165">Run demo applications</span></span>

<span data-ttu-id="3b04d-166">An ingress controller and a certificate management solution have been configured.</span><span class="sxs-lookup"><span data-stu-id="3b04d-166">An ingress controller and a certificate management solution have been configured.</span></span> <span data-ttu-id="3b04d-167">Now let's run two demo applications in your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="3b04d-167">Now let's run two demo applications in your AKS cluster.</span></span> <span data-ttu-id="3b04d-168">In this example, Helm is used to deploy two instances of a simple 'Hello world' application.</span><span class="sxs-lookup"><span data-stu-id="3b04d-168">In this example, Helm is used to deploy two instances of a simple 'Hello world' application.</span></span>

<span data-ttu-id="3b04d-169">Before you can install the sample Helm charts, add the Azure samples repository to your Helm environment as follows:</span><span class="sxs-lookup"><span data-stu-id="3b04d-169">Before you can install the sample Helm charts, add the Azure samples repository to your Helm environment as follows:</span></span>

```console
helm repo add azure-samples https://azure-samples.github.io/helm-charts/
```

<span data-ttu-id="3b04d-170">Create the first demo application from a Helm chart with the following command:</span><span class="sxs-lookup"><span data-stu-id="3b04d-170">Create the first demo application from a Helm chart with the following command:</span></span>

```console
helm install azure-samples/aks-helloworld
```

<span data-ttu-id="3b04d-171">Now install a second instance of the demo application.</span><span class="sxs-lookup"><span data-stu-id="3b04d-171">Now install a second instance of the demo application.</span></span> <span data-ttu-id="3b04d-172">For the second instance, you specify a new title so that the two applications are visually distinct.</span><span class="sxs-lookup"><span data-stu-id="3b04d-172">For the second instance, you specify a new title so that the two applications are visually distinct.</span></span> <span data-ttu-id="3b04d-173">You also specify a unique service name:</span><span class="sxs-lookup"><span data-stu-id="3b04d-173">You also specify a unique service name:</span></span>

```console
helm install azure-samples/aks-helloworld --set title="AKS Ingress Demo" --set serviceName="ingress-demo"
```

## <a name="create-an-ingress-route"></a><span data-ttu-id="3b04d-174">Create an ingress route</span><span class="sxs-lookup"><span data-stu-id="3b04d-174">Create an ingress route</span></span>

<span data-ttu-id="3b04d-175">Both applications are now running on your Kubernetes cluster, however they're configured with a service of type `ClusterIP`.</span><span class="sxs-lookup"><span data-stu-id="3b04d-175">Both applications are now running on your Kubernetes cluster, however they're configured with a service of type `ClusterIP`.</span></span> <span data-ttu-id="3b04d-176">As such, the applications aren't accessible from the internet.</span><span class="sxs-lookup"><span data-stu-id="3b04d-176">As such, the applications aren't accessible from the internet.</span></span> <span data-ttu-id="3b04d-177">To make them publicly available, create a Kubernetes ingress resource.</span><span class="sxs-lookup"><span data-stu-id="3b04d-177">To make them publicly available, create a Kubernetes ingress resource.</span></span> <span data-ttu-id="3b04d-178">The ingress resource configures the rules that route traffic to one of the two applications.</span><span class="sxs-lookup"><span data-stu-id="3b04d-178">The ingress resource configures the rules that route traffic to one of the two applications.</span></span>

<span data-ttu-id="3b04d-179">In the following example, traffic to the address `https://demo-aks-ingress.eastus.cloudapp.azure.com/` is routed to the service named `aks-helloworld`.</span><span class="sxs-lookup"><span data-stu-id="3b04d-179">In the following example, traffic to the address `https://demo-aks-ingress.eastus.cloudapp.azure.com/` is routed to the service named `aks-helloworld`.</span></span> <span data-ttu-id="3b04d-180">Traffic to the address `https://demo-aks-ingress.eastus.cloudapp.azure.com/hello-world-two` is routed to the `ingress-demo` service.</span><span class="sxs-lookup"><span data-stu-id="3b04d-180">Traffic to the address `https://demo-aks-ingress.eastus.cloudapp.azure.com/hello-world-two` is routed to the `ingress-demo` service.</span></span> <span data-ttu-id="3b04d-181">Update the *hosts* and *host* to the DNS name you created in a previous step.</span><span class="sxs-lookup"><span data-stu-id="3b04d-181">Update the *hosts* and *host* to the DNS name you created in a previous step.</span></span>

<span data-ttu-id="3b04d-182">Create a file named `hello-world-ingress.yaml` and copy in the following example YAML.</span><span class="sxs-lookup"><span data-stu-id="3b04d-182">Create a file named `hello-world-ingress.yaml` and copy in the following example YAML.</span></span>

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: hello-world-ingress
  annotations:
    kubernetes.io/ingress.class: nginx
    certmanager.k8s.io/cluster-issuer: letsencrypt-staging
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  tls:
  - hosts:
    - demo-aks-ingress.eastus.cloudapp.azure.com
    secretName: tls-secret
  rules:
  - host: demo-aks-ingress.eastus.cloudapp.azure.com
    http:
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

<span data-ttu-id="3b04d-183">Create the ingress resource using the `kubectl apply -f hello-world-ingress.yaml` command.</span><span class="sxs-lookup"><span data-stu-id="3b04d-183">Create the ingress resource using the `kubectl apply -f hello-world-ingress.yaml` command.</span></span>

```
$ kubectl apply -f hello-world-ingress.yaml

ingress.extensions/hello-world-ingress created
```

## <a name="test-the-ingress-configuration"></a><span data-ttu-id="3b04d-184">Test the ingress configuration</span><span class="sxs-lookup"><span data-stu-id="3b04d-184">Test the ingress configuration</span></span>

<span data-ttu-id="3b04d-185">Open a web browser to the FQDN of your Kubernetes ingress controller, such as *https://demo-aks-ingress.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="3b04d-185">Open a web browser to the FQDN of your Kubernetes ingress controller, such as *https://demo-aks-ingress.eastus.cloudapp.azure.com*.</span></span>

<span data-ttu-id="3b04d-186">As these examples use `letsencrypt-staging`, the issued SSL certificate is not trusted by the browser.</span><span class="sxs-lookup"><span data-stu-id="3b04d-186">As these examples use `letsencrypt-staging`, the issued SSL certificate is not trusted by the browser.</span></span> <span data-ttu-id="3b04d-187">Accept the warning prompt to continue to your application.</span><span class="sxs-lookup"><span data-stu-id="3b04d-187">Accept the warning prompt to continue to your application.</span></span> <span data-ttu-id="3b04d-188">The certificate information shows this *Fake LE Intermediate X1* certificate is issued by Let's Encrypt.</span><span class="sxs-lookup"><span data-stu-id="3b04d-188">The certificate information shows this *Fake LE Intermediate X1* certificate is issued by Let's Encrypt.</span></span> <span data-ttu-id="3b04d-189">This fake certificate indicates `cert-manager` processed the request correctly and received a certificate from the provider:</span><span class="sxs-lookup"><span data-stu-id="3b04d-189">This fake certificate indicates `cert-manager` processed the request correctly and received a certificate from the provider:</span></span>

![Let's Encrypt staging certificate](media/ingress/staging-certificate.png)

<span data-ttu-id="3b04d-191">When you change Let's Encrypt to use `prod` rather than `staging`, a trusted certificate issued by Let's Encrypt is used, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="3b04d-191">When you change Let's Encrypt to use `prod` rather than `staging`, a trusted certificate issued by Let's Encrypt is used, as shown in the following example:</span></span>

![Let's Encrypt certificate](media/ingress/certificate.png)

<span data-ttu-id="3b04d-193">The demo application is shown in the web browser:</span><span class="sxs-lookup"><span data-stu-id="3b04d-193">The demo application is shown in the web browser:</span></span>

![Application example one](media/ingress/app-one.png)

<span data-ttu-id="3b04d-195">Now add the */hello-world-two* path to the FQDN, such as *https://demo-aks-ingress.eastus.cloudapp.azure.com/hello-world-two*.</span><span class="sxs-lookup"><span data-stu-id="3b04d-195">Now add the */hello-world-two* path to the FQDN, such as *https://demo-aks-ingress.eastus.cloudapp.azure.com/hello-world-two*.</span></span> <span data-ttu-id="3b04d-196">The second demo application with the custom title is shown:</span><span class="sxs-lookup"><span data-stu-id="3b04d-196">The second demo application with the custom title is shown:</span></span>

![Application example two](media/ingress/app-two.png)

## <a name="next-steps"></a><span data-ttu-id="3b04d-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="3b04d-198">Next steps</span></span>

<span data-ttu-id="3b04d-199">This article included some external components to AKS.</span><span class="sxs-lookup"><span data-stu-id="3b04d-199">This article included some external components to AKS.</span></span> <span data-ttu-id="3b04d-200">To learn more about these components, see the following project pages:</span><span class="sxs-lookup"><span data-stu-id="3b04d-200">To learn more about these components, see the following project pages:</span></span>

- <span data-ttu-id="3b04d-201">[Helm CLI][helm-cli]</span><span class="sxs-lookup"><span data-stu-id="3b04d-201">[Helm CLI][helm-cli]</span></span>
- <span data-ttu-id="3b04d-202">[NGINX ingress controller][nginx-ingress]</span><span class="sxs-lookup"><span data-stu-id="3b04d-202">[NGINX ingress controller][nginx-ingress]</span></span>
- <span data-ttu-id="3b04d-203">[cert-manager][cert-manager]</span><span class="sxs-lookup"><span data-stu-id="3b04d-203">[cert-manager][cert-manager]</span></span>

<span data-ttu-id="3b04d-204">You can also:</span><span class="sxs-lookup"><span data-stu-id="3b04d-204">You can also:</span></span>

- <span data-ttu-id="3b04d-205">[Create a basic ingress controller with external network connectivity][aks-ingress-basic]</span><span class="sxs-lookup"><span data-stu-id="3b04d-205">[Create a basic ingress controller with external network connectivity][aks-ingress-basic]</span></span>
- <span data-ttu-id="3b04d-206">[Enable the HTTP application routing add-on][aks-http-app-routing]</span><span class="sxs-lookup"><span data-stu-id="3b04d-206">[Enable the HTTP application routing add-on][aks-http-app-routing]</span></span>
- <span data-ttu-id="3b04d-207">[Create an ingress controller that uses an internal, private network and IP address][aks-ingress-internal]</span><span class="sxs-lookup"><span data-stu-id="3b04d-207">[Create an ingress controller that uses an internal, private network and IP address][aks-ingress-internal]</span></span>
- <span data-ttu-id="3b04d-208">[Create an ingress controller with a static public IP address and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-static-tls]</span><span class="sxs-lookup"><span data-stu-id="3b04d-208">[Create an ingress controller with a static public IP address and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-static-tls]</span></span>

<!-- LINKS - external -->
[helm-cli]: https://docs.microsoft.com/azure/aks/kubernetes-helm#install-helm-cli
[cert-manager]: https://github.com/jetstack/cert-manager
[cert-manager-certificates]: https://cert-manager.readthedocs.io/en/latest/reference/certificates.html
[cert-manager-cluster-issuer]: https://cert-manager.readthedocs.io/en/latest/reference/clusterissuers.html
[cert-manager-issuer]: https://cert-manager.readthedocs.io/en/latest/reference/issuers.html
[lets-encrypt]: https://letsencrypt.org/
[nginx-ingress]: https://github.com/kubernetes/ingress-nginx
[helm-install]: https://docs.helm.sh/using_helm/#installing-helm

<!-- LINKS - internal -->
[use-helm]: kubernetes-helm.md
[azure-cli-install]: /cli/azure/install-azure-cli
[az-aks-show]: /cli/azure/aks#az-aks-show
[az-network-public-ip-create]: /cli/azure/network/public-ip#az-network-public-ip-create
[aks-ingress-internal]: ingress-internal-ip.md
[aks-ingress-static-tls]: ingress-static-ip.md
[aks-ingress-basic]: ingress-basic.md
[aks-http-app-routing]: http-application-routing.md
