---
title: Create an HTTP ingress controller with a static IP address in Azure Kubernetes Service (AKS)
description: Learn how to install and configure an NGINX ingress controller with a static public IP address in an Azure Kubernetes Service (AKS) cluster.
services: container-service
author: iainfoulds
ms.service: container-service
ms.topic: article
ms.date: 08/30/2018
ms.author: iainfou
ms.openlocfilehash: 9bcfa7996b301ea5ff26464315b16a08e054ba60
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866427"
---
# <a name="create-an-ingress-controller-with-a-static-public-ip-address-in-azure-kubernetes-service-aks"></a><span data-ttu-id="95423-103">Create an ingress controller with a static public IP address in Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="95423-103">Create an ingress controller with a static public IP address in Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="95423-104">An ingress controller is a piece of software that provides reverse proxy, configurable traffic routing, and TLS termination for Kubernetes services.</span><span class="sxs-lookup"><span data-stu-id="95423-104">An ingress controller is a piece of software that provides reverse proxy, configurable traffic routing, and TLS termination for Kubernetes services.</span></span> <span data-ttu-id="95423-105">Kubernetes ingress resources are used to configure the ingress rules and routes for individual Kubernetes services.</span><span class="sxs-lookup"><span data-stu-id="95423-105">Kubernetes ingress resources are used to configure the ingress rules and routes for individual Kubernetes services.</span></span> <span data-ttu-id="95423-106">Using an ingress controller and ingress rules, a single IP address can be used to route traffic to multiple services in a Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="95423-106">Using an ingress controller and ingress rules, a single IP address can be used to route traffic to multiple services in a Kubernetes cluster.</span></span>

<span data-ttu-id="95423-107">This article shows you how to deploy the [NGINX ingress controller][nginx-ingress] in an Azure Kubernetes Service (AKS) cluster.</span><span class="sxs-lookup"><span data-stu-id="95423-107">This article shows you how to deploy the [NGINX ingress controller][nginx-ingress] in an Azure Kubernetes Service (AKS) cluster.</span></span> <span data-ttu-id="95423-108">The ingress controller is configured with a static public IP address.</span><span class="sxs-lookup"><span data-stu-id="95423-108">The ingress controller is configured with a static public IP address.</span></span> <span data-ttu-id="95423-109">The [cert-manager][cert-manager] project is used to automatically generate and configure [Let's Encrypt][lets-encrypt] certificates.</span><span class="sxs-lookup"><span data-stu-id="95423-109">The [cert-manager][cert-manager] project is used to automatically generate and configure [Let's Encrypt][lets-encrypt] certificates.</span></span> <span data-ttu-id="95423-110">Finally, two applications are run in the AKS cluster, each of which is accessible over a single IP address.</span><span class="sxs-lookup"><span data-stu-id="95423-110">Finally, two applications are run in the AKS cluster, each of which is accessible over a single IP address.</span></span>

<span data-ttu-id="95423-111">You can also:</span><span class="sxs-lookup"><span data-stu-id="95423-111">You can also:</span></span>

- <span data-ttu-id="95423-112">[Create a basic ingress controller with external network connectivity][aks-ingress-basic]</span><span class="sxs-lookup"><span data-stu-id="95423-112">[Create a basic ingress controller with external network connectivity][aks-ingress-basic]</span></span>
- <span data-ttu-id="95423-113">[Enable the HTTP application routing add-on][aks-http-app-routing]</span><span class="sxs-lookup"><span data-stu-id="95423-113">[Enable the HTTP application routing add-on][aks-http-app-routing]</span></span>
- <span data-ttu-id="95423-114">[Create an ingress controller that uses an internal, private network and IP address][aks-ingress-internal]</span><span class="sxs-lookup"><span data-stu-id="95423-114">[Create an ingress controller that uses an internal, private network and IP address][aks-ingress-internal]</span></span>
- <span data-ttu-id="95423-115">[Create an ingress controller with a dynamic public IP and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-tls]</span><span class="sxs-lookup"><span data-stu-id="95423-115">[Create an ingress controller with a dynamic public IP and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-tls]</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="95423-116">Before you begin</span><span class="sxs-lookup"><span data-stu-id="95423-116">Before you begin</span></span>

<span data-ttu-id="95423-117">This article uses Helm to install the NGINX ingress controller, cert-manager, and a sample web app.</span><span class="sxs-lookup"><span data-stu-id="95423-117">This article uses Helm to install the NGINX ingress controller, cert-manager, and a sample web app.</span></span> <span data-ttu-id="95423-118">You need to have Helm initialized within your AKS cluster and using a service account for Tiller.</span><span class="sxs-lookup"><span data-stu-id="95423-118">You need to have Helm initialized within your AKS cluster and using a service account for Tiller.</span></span> <span data-ttu-id="95423-119">Make sure that you are using the latest release of Helm.</span><span class="sxs-lookup"><span data-stu-id="95423-119">Make sure that you are using the latest release of Helm.</span></span> <span data-ttu-id="95423-120">Make sure that you are using the latest release of Helm.</span><span class="sxs-lookup"><span data-stu-id="95423-120">Make sure that you are using the latest release of Helm.</span></span> <span data-ttu-id="95423-121">For upgrade instructions, see the [Helm install docs][helm-install]. For more information on configuring and using Helm, see [Install applications with Helm in Azure Kubernetes Service (AKS)][use-helm].</span><span class="sxs-lookup"><span data-stu-id="95423-121">For upgrade instructions, see the [Helm install docs][helm-install]. For more information on configuring and using Helm, see [Install applications with Helm in Azure Kubernetes Service (AKS)][use-helm].</span></span>

<span data-ttu-id="95423-122">This article also requires that you are running the Azure CLI version 2.0.41 or later.</span><span class="sxs-lookup"><span data-stu-id="95423-122">This article also requires that you are running the Azure CLI version 2.0.41 or later.</span></span> <span data-ttu-id="95423-123">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="95423-123">Run `az --version` to find the version.</span></span> <span data-ttu-id="95423-124">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span><span class="sxs-lookup"><span data-stu-id="95423-124">If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].</span></span>

## <a name="create-an-ingress-controller"></a><span data-ttu-id="95423-125">Create an ingress controller</span><span class="sxs-lookup"><span data-stu-id="95423-125">Create an ingress controller</span></span>

<span data-ttu-id="95423-126">By default, an NGINX ingress controller is created with a new public IP address assignment.</span><span class="sxs-lookup"><span data-stu-id="95423-126">By default, an NGINX ingress controller is created with a new public IP address assignment.</span></span> <span data-ttu-id="95423-127">This public IP address is only static for the life-span of the ingress controller, and is lost if the controller is deleted and re-created.</span><span class="sxs-lookup"><span data-stu-id="95423-127">This public IP address is only static for the life-span of the ingress controller, and is lost if the controller is deleted and re-created.</span></span> <span data-ttu-id="95423-128">A common configuration requirement is to provide the NGINX ingress controller an existing static public IP address.</span><span class="sxs-lookup"><span data-stu-id="95423-128">A common configuration requirement is to provide the NGINX ingress controller an existing static public IP address.</span></span> <span data-ttu-id="95423-129">The static public IP address remains if the ingress controller is deleted.</span><span class="sxs-lookup"><span data-stu-id="95423-129">The static public IP address remains if the ingress controller is deleted.</span></span> <span data-ttu-id="95423-130">This approach allows you to use existing DNS records and network configurations in a consistent manner throughout the lifecycle of your applications.</span><span class="sxs-lookup"><span data-stu-id="95423-130">This approach allows you to use existing DNS records and network configurations in a consistent manner throughout the lifecycle of your applications.</span></span>

<span data-ttu-id="95423-131">If you need to create a static public IP address, first get the resource group name of the AKS cluster with the [az aks show][az-aks-show] command:</span><span class="sxs-lookup"><span data-stu-id="95423-131">If you need to create a static public IP address, first get the resource group name of the AKS cluster with the [az aks show][az-aks-show] command:</span></span>

```azurecli
az aks show --resource-group myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv
```

<span data-ttu-id="95423-132">Next, create a public IP address with the *static* allocation method using the [az network public-ip create][az-network-public-ip-create] command.</span><span class="sxs-lookup"><span data-stu-id="95423-132">Next, create a public IP address with the *static* allocation method using the [az network public-ip create][az-network-public-ip-create] command.</span></span> <span data-ttu-id="95423-133">The following example creates a public IP address named *myAKSPublicIP* in the AKS cluster resource group obtained in the previous step:</span><span class="sxs-lookup"><span data-stu-id="95423-133">The following example creates a public IP address named *myAKSPublicIP* in the AKS cluster resource group obtained in the previous step:</span></span>

```azurecli
az network public-ip create --resource-group MC_myResourceGroup_myAKSCluster_eastus --name myAKSPublicIP --allocation-method static
```

<span data-ttu-id="95423-134">Now deploy the *nginx-ingress* chart with Helm.</span><span class="sxs-lookup"><span data-stu-id="95423-134">Now deploy the *nginx-ingress* chart with Helm.</span></span> <span data-ttu-id="95423-135">Add the `--set controller.service.loadBalancerIP` parameter, and specify your own public IP address created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="95423-135">Add the `--set controller.service.loadBalancerIP` parameter, and specify your own public IP address created in the previous step.</span></span>

> [!TIP]
> <span data-ttu-id="95423-136">The following example installs the ingress controller in the `kube-system` namespace.</span><span class="sxs-lookup"><span data-stu-id="95423-136">The following example installs the ingress controller in the `kube-system` namespace.</span></span> <span data-ttu-id="95423-137">You can specify a different namespace for your own environment if desired.</span><span class="sxs-lookup"><span data-stu-id="95423-137">You can specify a different namespace for your own environment if desired.</span></span> <span data-ttu-id="95423-138">If your AKS cluster is not RBAC enabled, add `--set rbac.create=false` to the commands.</span><span class="sxs-lookup"><span data-stu-id="95423-138">If your AKS cluster is not RBAC enabled, add `--set rbac.create=false` to the commands.</span></span>

```console
helm install stable/nginx-ingress --namespace kube-system --set controller.service.loadBalancerIP="40.121.63.72"
```

<span data-ttu-id="95423-139">When the Kubernetes load balancer service is created for the NGINX ingress controller, your static IP address is assigned, as shown in the following example output:</span><span class="sxs-lookup"><span data-stu-id="95423-139">When the Kubernetes load balancer service is created for the NGINX ingress controller, your static IP address is assigned, as shown in the following example output:</span></span>

```
$ kubectl get service -l app=nginx-ingress --namespace kube-system

NAME                                        TYPE           CLUSTER-IP    EXTERNAL-IP    PORT(S)                      AGE
dinky-panda-nginx-ingress-controller        LoadBalancer   10.0.232.56   40.121.63.72   80:31978/TCP,443:32037/TCP   3m
dinky-panda-nginx-ingress-default-backend   ClusterIP      10.0.95.248   <none>         80/TCP                       3m
```

<span data-ttu-id="95423-140">No ingress rules have been created yet, so the NGINX ingress controller's default 404 page is displayed if you browse to the public IP address.</span><span class="sxs-lookup"><span data-stu-id="95423-140">No ingress rules have been created yet, so the NGINX ingress controller's default 404 page is displayed if you browse to the public IP address.</span></span> <span data-ttu-id="95423-141">Ingress rules are configured in the following steps.</span><span class="sxs-lookup"><span data-stu-id="95423-141">Ingress rules are configured in the following steps.</span></span>

## <a name="configure-a-dns-name"></a><span data-ttu-id="95423-142">Configure a DNS name</span><span class="sxs-lookup"><span data-stu-id="95423-142">Configure a DNS name</span></span>

<span data-ttu-id="95423-143">For the HTTPS certificates to work correctly, configure an FQDN for the ingress controller IP address.</span><span class="sxs-lookup"><span data-stu-id="95423-143">For the HTTPS certificates to work correctly, configure an FQDN for the ingress controller IP address.</span></span> <span data-ttu-id="95423-144">Update the following script with the IP address of your ingress controller and a unique name that you would like to use for the FQDN:</span><span class="sxs-lookup"><span data-stu-id="95423-144">Update the following script with the IP address of your ingress controller and a unique name that you would like to use for the FQDN:</span></span>

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

<span data-ttu-id="95423-145">The ingress controller is now accessible through the FQDN.</span><span class="sxs-lookup"><span data-stu-id="95423-145">The ingress controller is now accessible through the FQDN.</span></span>

## <a name="install-cert-manager"></a><span data-ttu-id="95423-146">Install cert-manager</span><span class="sxs-lookup"><span data-stu-id="95423-146">Install cert-manager</span></span>

<span data-ttu-id="95423-147">The NGINX ingress controller supports TLS termination.</span><span class="sxs-lookup"><span data-stu-id="95423-147">The NGINX ingress controller supports TLS termination.</span></span> <span data-ttu-id="95423-148">There are several ways to retrieve and configure certificates for HTTPS.</span><span class="sxs-lookup"><span data-stu-id="95423-148">There are several ways to retrieve and configure certificates for HTTPS.</span></span> <span data-ttu-id="95423-149">This article demonstrates using [cert-manager][cert-manager], which provides automatic [Lets Encrypt][lets-encrypt] certificate generation and management functionality.</span><span class="sxs-lookup"><span data-stu-id="95423-149">This article demonstrates using [cert-manager][cert-manager], which provides automatic [Lets Encrypt][lets-encrypt] certificate generation and management functionality.</span></span>

> [!NOTE]
> <span data-ttu-id="95423-150">This article uses the `staging` environment for Let's Encrypt.</span><span class="sxs-lookup"><span data-stu-id="95423-150">This article uses the `staging` environment for Let's Encrypt.</span></span> <span data-ttu-id="95423-151">In production deployments, use `letsencrypt-prod` and `https://acme-v02.api.letsencrypt.org/directory` in the resource definitions and when installing the Helm chart.</span><span class="sxs-lookup"><span data-stu-id="95423-151">In production deployments, use `letsencrypt-prod` and `https://acme-v02.api.letsencrypt.org/directory` in the resource definitions and when installing the Helm chart.</span></span>

<span data-ttu-id="95423-152">To install the cert-manager controller in an RBAC-enabled cluster, use the following `helm install` command:</span><span class="sxs-lookup"><span data-stu-id="95423-152">To install the cert-manager controller in an RBAC-enabled cluster, use the following `helm install` command:</span></span>

```console
helm install stable/cert-manager --set ingressShim.defaultIssuerName=letsencrypt-staging --set ingressShim.defaultIssuerKind=ClusterIssuer
```

<span data-ttu-id="95423-153">If your cluster is not RBAC enabled, instead use the following command:</span><span class="sxs-lookup"><span data-stu-id="95423-153">If your cluster is not RBAC enabled, instead use the following command:</span></span>

```console
helm install stable/cert-manager \
  --set ingressShim.defaultIssuerName=letsencrypt-staging \
  --set ingressShim.defaultIssuerKind=ClusterIssuer \
  --set rbac.create=false \
  --set serviceAccount.create=false
```

<span data-ttu-id="95423-154">For more information on cert-manager configuration, see the [cert-manager project][cert-manager].</span><span class="sxs-lookup"><span data-stu-id="95423-154">For more information on cert-manager configuration, see the [cert-manager project][cert-manager].</span></span>

## <a name="create-a-ca-cluster-issuer"></a><span data-ttu-id="95423-155">Create a CA cluster issuer</span><span class="sxs-lookup"><span data-stu-id="95423-155">Create a CA cluster issuer</span></span>

<span data-ttu-id="95423-156">Before certificates can be issued, cert-manager requires an [Issuer][cert-manager-issuer] or [ClusterIssuer][cert-manager-cluster-issuer] resource.</span><span class="sxs-lookup"><span data-stu-id="95423-156">Before certificates can be issued, cert-manager requires an [Issuer][cert-manager-issuer] or [ClusterIssuer][cert-manager-cluster-issuer] resource.</span></span> <span data-ttu-id="95423-157">These Kubernetes resources are identical in functionality, however `Issuer` works in a single namespace, and `ClusterIssuer` works across all namespaces.</span><span class="sxs-lookup"><span data-stu-id="95423-157">These Kubernetes resources are identical in functionality, however `Issuer` works in a single namespace, and `ClusterIssuer` works across all namespaces.</span></span> <span data-ttu-id="95423-158">For more information, see the [cert-manager issuer][cert-manager-issuer] documentation.</span><span class="sxs-lookup"><span data-stu-id="95423-158">For more information, see the [cert-manager issuer][cert-manager-issuer] documentation.</span></span>

<span data-ttu-id="95423-159">Create a cluster issuer, such as `cluster-issuer.yaml`, using the following example manifest.</span><span class="sxs-lookup"><span data-stu-id="95423-159">Create a cluster issuer, such as `cluster-issuer.yaml`, using the following example manifest.</span></span> <span data-ttu-id="95423-160">Update the email address with a valid address from your organization:</span><span class="sxs-lookup"><span data-stu-id="95423-160">Update the email address with a valid address from your organization:</span></span>

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

<span data-ttu-id="95423-161">To create the issuer, use the `kubectl apply -f cluster-issuer.yaml` command.</span><span class="sxs-lookup"><span data-stu-id="95423-161">To create the issuer, use the `kubectl apply -f cluster-issuer.yaml` command.</span></span>

```
$ kubectl apply -f cluster-issuer.yaml

clusterissuer.certmanager.k8s.io/letsencrypt-staging created
```

## <a name="create-a-certificate-object"></a><span data-ttu-id="95423-162">Create a certificate object</span><span class="sxs-lookup"><span data-stu-id="95423-162">Create a certificate object</span></span>

<span data-ttu-id="95423-163">Next, a certificate resource must be created.</span><span class="sxs-lookup"><span data-stu-id="95423-163">Next, a certificate resource must be created.</span></span> <span data-ttu-id="95423-164">The certificate resource defines the desired X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="95423-164">The certificate resource defines the desired X.509 certificate.</span></span> <span data-ttu-id="95423-165">For more information, see [cert-manager certificates][cert-manager-certificates].</span><span class="sxs-lookup"><span data-stu-id="95423-165">For more information, see [cert-manager certificates][cert-manager-certificates].</span></span>

<span data-ttu-id="95423-166">Create the certificate resource, such as `certificates.yaml`, with the following example manifest.</span><span class="sxs-lookup"><span data-stu-id="95423-166">Create the certificate resource, such as `certificates.yaml`, with the following example manifest.</span></span> <span data-ttu-id="95423-167">Update the *dnsNames* and *domains* to the DNS name you created in a previous step.</span><span class="sxs-lookup"><span data-stu-id="95423-167">Update the *dnsNames* and *domains* to the DNS name you created in a previous step.</span></span> <span data-ttu-id="95423-168">If you use an internal-only ingress controller, specify the internal DNS name for your service.</span><span class="sxs-lookup"><span data-stu-id="95423-168">If you use an internal-only ingress controller, specify the internal DNS name for your service.</span></span>

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

<span data-ttu-id="95423-169">To create the certificate resource, use the `kubectl apply -f certificates.yaml` command.</span><span class="sxs-lookup"><span data-stu-id="95423-169">To create the certificate resource, use the `kubectl apply -f certificates.yaml` command.</span></span>

```
$ kubectl apply -f certificates.yaml

certificate.certmanager.k8s.io/tls-secret created
```

## <a name="run-demo-applications"></a><span data-ttu-id="95423-170">Run demo applications</span><span class="sxs-lookup"><span data-stu-id="95423-170">Run demo applications</span></span>

<span data-ttu-id="95423-171">An ingress controller and a certificate management solution have been configured.</span><span class="sxs-lookup"><span data-stu-id="95423-171">An ingress controller and a certificate management solution have been configured.</span></span> <span data-ttu-id="95423-172">Now let's run two demo applications in your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="95423-172">Now let's run two demo applications in your AKS cluster.</span></span> <span data-ttu-id="95423-173">In this example, Helm is used to deploy two instances of a simple 'Hello world' application.</span><span class="sxs-lookup"><span data-stu-id="95423-173">In this example, Helm is used to deploy two instances of a simple 'Hello world' application.</span></span>

<span data-ttu-id="95423-174">Before you can install the sample Helm charts, add the Azure samples repository to your Helm environment as follows:</span><span class="sxs-lookup"><span data-stu-id="95423-174">Before you can install the sample Helm charts, add the Azure samples repository to your Helm environment as follows:</span></span>

```console
helm repo add azure-samples https://azure-samples.github.io/helm-charts/
```

<span data-ttu-id="95423-175">Create the first demo application from a Helm chart with the following command:</span><span class="sxs-lookup"><span data-stu-id="95423-175">Create the first demo application from a Helm chart with the following command:</span></span>

```console
helm install azure-samples/aks-helloworld
```

<span data-ttu-id="95423-176">Now install a second instance of the demo application.</span><span class="sxs-lookup"><span data-stu-id="95423-176">Now install a second instance of the demo application.</span></span> <span data-ttu-id="95423-177">For the second instance, you specify a new title so that the two applications are visually distinct.</span><span class="sxs-lookup"><span data-stu-id="95423-177">For the second instance, you specify a new title so that the two applications are visually distinct.</span></span> <span data-ttu-id="95423-178">You also specify a unique service name:</span><span class="sxs-lookup"><span data-stu-id="95423-178">You also specify a unique service name:</span></span>

```console
helm install azure-samples/aks-helloworld --set title="AKS Ingress Demo" --set serviceName="ingress-demo"
```

## <a name="create-an-ingress-route"></a><span data-ttu-id="95423-179">Create an ingress route</span><span class="sxs-lookup"><span data-stu-id="95423-179">Create an ingress route</span></span>

<span data-ttu-id="95423-180">Both applications are now running on your Kubernetes cluster, however they're configured with a service of type `ClusterIP`.</span><span class="sxs-lookup"><span data-stu-id="95423-180">Both applications are now running on your Kubernetes cluster, however they're configured with a service of type `ClusterIP`.</span></span> <span data-ttu-id="95423-181">As such, the applications aren't accessible from the internet.</span><span class="sxs-lookup"><span data-stu-id="95423-181">As such, the applications aren't accessible from the internet.</span></span> <span data-ttu-id="95423-182">To make them publicly available, create a Kubernetes ingress resource.</span><span class="sxs-lookup"><span data-stu-id="95423-182">To make them publicly available, create a Kubernetes ingress resource.</span></span> <span data-ttu-id="95423-183">The ingress resource configures the rules that route traffic to one of the two applications.</span><span class="sxs-lookup"><span data-stu-id="95423-183">The ingress resource configures the rules that route traffic to one of the two applications.</span></span>

<span data-ttu-id="95423-184">In the following example, traffic to the address `https://demo-aks-ingress.eastus.cloudapp.azure.com/` is routed to the service named `aks-helloworld`.</span><span class="sxs-lookup"><span data-stu-id="95423-184">In the following example, traffic to the address `https://demo-aks-ingress.eastus.cloudapp.azure.com/` is routed to the service named `aks-helloworld`.</span></span> <span data-ttu-id="95423-185">Traffic to the address `https://demo-aks-ingress.eastus.cloudapp.azure.com/hello-world-two` is routed to the `ingress-demo` service.</span><span class="sxs-lookup"><span data-stu-id="95423-185">Traffic to the address `https://demo-aks-ingress.eastus.cloudapp.azure.com/hello-world-two` is routed to the `ingress-demo` service.</span></span> <span data-ttu-id="95423-186">Update the *hosts* and *host* to the DNS name you created in a previous step.</span><span class="sxs-lookup"><span data-stu-id="95423-186">Update the *hosts* and *host* to the DNS name you created in a previous step.</span></span>

<span data-ttu-id="95423-187">Create a file named `hello-world-ingress.yaml` and copy in the following example YAML.</span><span class="sxs-lookup"><span data-stu-id="95423-187">Create a file named `hello-world-ingress.yaml` and copy in the following example YAML.</span></span>

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

<span data-ttu-id="95423-188">Create the ingress resource using the `kubectl apply -f hello-world-ingress.yaml` command.</span><span class="sxs-lookup"><span data-stu-id="95423-188">Create the ingress resource using the `kubectl apply -f hello-world-ingress.yaml` command.</span></span>

```
$ kubectl apply -f hello-world-ingress.yaml

ingress.extensions/hello-world-ingress created
```

## <a name="test-the-ingress-configuration"></a><span data-ttu-id="95423-189">Test the ingress configuration</span><span class="sxs-lookup"><span data-stu-id="95423-189">Test the ingress configuration</span></span>

<span data-ttu-id="95423-190">Open a web browser to the FQDN of your Kubernetes ingress controller, such as *https://demo-aks-ingress.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="95423-190">Open a web browser to the FQDN of your Kubernetes ingress controller, such as *https://demo-aks-ingress.eastus.cloudapp.azure.com*.</span></span>

<span data-ttu-id="95423-191">As these examples use `letsencrypt-staging`, the issued SSL certificate is not trusted by the browser.</span><span class="sxs-lookup"><span data-stu-id="95423-191">As these examples use `letsencrypt-staging`, the issued SSL certificate is not trusted by the browser.</span></span> <span data-ttu-id="95423-192">Accept the warning prompt to continue to your application.</span><span class="sxs-lookup"><span data-stu-id="95423-192">Accept the warning prompt to continue to your application.</span></span> <span data-ttu-id="95423-193">The certificate information shows this *Fake LE Intermediate X1* certificate is issued by Let's Encrypt.</span><span class="sxs-lookup"><span data-stu-id="95423-193">The certificate information shows this *Fake LE Intermediate X1* certificate is issued by Let's Encrypt.</span></span> <span data-ttu-id="95423-194">This fake certificate indicates `cert-manager` processed the request correctly and received a certificate from the provider:</span><span class="sxs-lookup"><span data-stu-id="95423-194">This fake certificate indicates `cert-manager` processed the request correctly and received a certificate from the provider:</span></span>

![Let's Encrypt staging certificate](media/ingress/staging-certificate.png)

<span data-ttu-id="95423-196">When you change Let's Encrypt to use `prod` rather than `staging`, a trusted certificate issued by Let's Encrypt is used, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="95423-196">When you change Let's Encrypt to use `prod` rather than `staging`, a trusted certificate issued by Let's Encrypt is used, as shown in the following example:</span></span>

![Let's Encrypt certificate](media/ingress/certificate.png)

<span data-ttu-id="95423-198">The demo application is shown in the web browser:</span><span class="sxs-lookup"><span data-stu-id="95423-198">The demo application is shown in the web browser:</span></span>

![Application example one](media/ingress/app-one.png)

<span data-ttu-id="95423-200">Now add the */hello-world-two* path to the FQDN, such as *https://demo-aks-ingress.eastus.cloudapp.azure.com/hello-world-two*.</span><span class="sxs-lookup"><span data-stu-id="95423-200">Now add the */hello-world-two* path to the FQDN, such as *https://demo-aks-ingress.eastus.cloudapp.azure.com/hello-world-two*.</span></span> <span data-ttu-id="95423-201">The second demo application with the custom title is shown:</span><span class="sxs-lookup"><span data-stu-id="95423-201">The second demo application with the custom title is shown:</span></span>

![Application example two](media/ingress/app-two.png)

## <a name="next-steps"></a><span data-ttu-id="95423-203">Next steps</span><span class="sxs-lookup"><span data-stu-id="95423-203">Next steps</span></span>

<span data-ttu-id="95423-204">This article included some external components to AKS.</span><span class="sxs-lookup"><span data-stu-id="95423-204">This article included some external components to AKS.</span></span> <span data-ttu-id="95423-205">To learn more about these components, see the following project pages:</span><span class="sxs-lookup"><span data-stu-id="95423-205">To learn more about these components, see the following project pages:</span></span>

- <span data-ttu-id="95423-206">[Helm CLI][helm-cli]</span><span class="sxs-lookup"><span data-stu-id="95423-206">[Helm CLI][helm-cli]</span></span>
- <span data-ttu-id="95423-207">[NGINX ingress controller][nginx-ingress]</span><span class="sxs-lookup"><span data-stu-id="95423-207">[NGINX ingress controller][nginx-ingress]</span></span>
- <span data-ttu-id="95423-208">[cert-manager][cert-manager]</span><span class="sxs-lookup"><span data-stu-id="95423-208">[cert-manager][cert-manager]</span></span>

<span data-ttu-id="95423-209">You can also:</span><span class="sxs-lookup"><span data-stu-id="95423-209">You can also:</span></span>

- <span data-ttu-id="95423-210">[Create a basic ingress controller with external network connectivity][aks-ingress-basic]</span><span class="sxs-lookup"><span data-stu-id="95423-210">[Create a basic ingress controller with external network connectivity][aks-ingress-basic]</span></span>
- <span data-ttu-id="95423-211">[Enable the HTTP application routing add-on][aks-http-app-routing]</span><span class="sxs-lookup"><span data-stu-id="95423-211">[Enable the HTTP application routing add-on][aks-http-app-routing]</span></span>
- <span data-ttu-id="95423-212">[Create an ingress controller that uses an internal, private network and IP address][aks-ingress-internal]</span><span class="sxs-lookup"><span data-stu-id="95423-212">[Create an ingress controller that uses an internal, private network and IP address][aks-ingress-internal]</span></span>
- <span data-ttu-id="95423-213">[Create an ingress controller with a dynamic public IP and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-tls]</span><span class="sxs-lookup"><span data-stu-id="95423-213">[Create an ingress controller with a dynamic public IP and configure Let's Encrypt to automatically generate TLS certificates][aks-ingress-tls]</span></span>

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
[aks-ingress-basic]: ingress-basic.md
[aks-ingress-tls]: ingress-tls.md
[aks-http-app-routing]: http-application-routing.md
