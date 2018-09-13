---
title: HTTP application routing add-on on Azure Kubernetes Service (AKS)
description: Use the HTTP application routing add-on on Azure Kubernetes Service (AKS).
services: container-service
author: lachie83
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 04/25/2018
ms.author: laevenso
ms.openlocfilehash: 8934852fe3d95d0a96af0283c30bba4b3bdb411b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856158"
---
# <a name="http-application-routing"></a><span data-ttu-id="21a11-103">HTTP application routing</span><span class="sxs-lookup"><span data-stu-id="21a11-103">HTTP application routing</span></span>

<span data-ttu-id="21a11-104">The HTTP application routing solution makes it easy to access applications that are deployed to your Azure Kubernetes Service (AKS) cluster.</span><span class="sxs-lookup"><span data-stu-id="21a11-104">The HTTP application routing solution makes it easy to access applications that are deployed to your Azure Kubernetes Service (AKS) cluster.</span></span> <span data-ttu-id="21a11-105">When the solution's enabled, it configures an Ingress controller in your AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="21a11-105">When the solution's enabled, it configures an Ingress controller in your AKS cluster.</span></span> <span data-ttu-id="21a11-106">As applications are deployed, the solution also creates publically accessible DNS names for application endpoints.</span><span class="sxs-lookup"><span data-stu-id="21a11-106">As applications are deployed, the solution also creates publically accessible DNS names for application endpoints.</span></span>

<span data-ttu-id="21a11-107">When the add-on is enabled, it creates a DNS Zone in your subscription.</span><span class="sxs-lookup"><span data-stu-id="21a11-107">When the add-on is enabled, it creates a DNS Zone in your subscription.</span></span> <span data-ttu-id="21a11-108">For more information about DNS cost, see [DNS pricing][dns-pricing].</span><span class="sxs-lookup"><span data-stu-id="21a11-108">For more information about DNS cost, see [DNS pricing][dns-pricing].</span></span>

## <a name="http-routing-solution-overview"></a><span data-ttu-id="21a11-109">HTTP routing solution overview</span><span class="sxs-lookup"><span data-stu-id="21a11-109">HTTP routing solution overview</span></span>

<span data-ttu-id="21a11-110">The add-on deploys two components: a [Kubernetes Ingress controller][ingress] and an [External-DNS][external-dns] controller.</span><span class="sxs-lookup"><span data-stu-id="21a11-110">The add-on deploys two components: a [Kubernetes Ingress controller][ingress] and an [External-DNS][external-dns] controller.</span></span>

- <span data-ttu-id="21a11-111">**Ingress controller**: The Ingress controller is exposed to the internet by using a Kubernetes service of type LoadBalancer.</span><span class="sxs-lookup"><span data-stu-id="21a11-111">**Ingress controller**: The Ingress controller is exposed to the internet by using a Kubernetes service of type LoadBalancer.</span></span> <span data-ttu-id="21a11-112">The Ingress controller watches and implements [Kubernetes Ingress resources][ingress-resource], which creates routes to application endpoints.</span><span class="sxs-lookup"><span data-stu-id="21a11-112">The Ingress controller watches and implements [Kubernetes Ingress resources][ingress-resource], which creates routes to application endpoints.</span></span>
- <span data-ttu-id="21a11-113">**External-DNS controller**: Watches for Kubernetes Ingress resources and creates DNS A records in the cluster-specific DNS zone.</span><span class="sxs-lookup"><span data-stu-id="21a11-113">**External-DNS controller**: Watches for Kubernetes Ingress resources and creates DNS A records in the cluster-specific DNS zone.</span></span>

## <a name="deploy-http-routing-cli"></a><span data-ttu-id="21a11-114">Deploy HTTP routing: CLI</span><span class="sxs-lookup"><span data-stu-id="21a11-114">Deploy HTTP routing: CLI</span></span>

<span data-ttu-id="21a11-115">The HTTP application routing add-on can be enabled with the Azure CLI when deploying an AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="21a11-115">The HTTP application routing add-on can be enabled with the Azure CLI when deploying an AKS cluster.</span></span> <span data-ttu-id="21a11-116">To do so, use the [az aks create][az-aks-create] command with the `--enable-addons` argument.</span><span class="sxs-lookup"><span data-stu-id="21a11-116">To do so, use the [az aks create][az-aks-create] command with the `--enable-addons` argument.</span></span>

```azurecli
az aks create --resource-group myResourceGroup --name myAKSCluster --enable-addons http_application_routing
```

<span data-ttu-id="21a11-117">You can also enable HTTP routing on an existing AKS cluster using the [az aks enable-addons][az-aks-enable-addons] command.</span><span class="sxs-lookup"><span data-stu-id="21a11-117">You can also enable HTTP routing on an existing AKS cluster using the [az aks enable-addons][az-aks-enable-addons] command.</span></span> <span data-ttu-id="21a11-118">To enable HTTP routing on an existing cluster, add the `--addons` parameter and specify *http_application_routing* as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="21a11-118">To enable HTTP routing on an existing cluster, add the `--addons` parameter and specify *http_application_routing* as shown in the following example:</span></span>

```azurecli
az aks enable-addons --resource-group myResourceGroup --name myAKSCluster --addons http_application_routing
```

<span data-ttu-id="21a11-119">After the cluster is deployed or updated, use the [az aks show][az-aks-show] command to retrieve the DNS zone name.</span><span class="sxs-lookup"><span data-stu-id="21a11-119">After the cluster is deployed or updated, use the [az aks show][az-aks-show] command to retrieve the DNS zone name.</span></span> <span data-ttu-id="21a11-120">This name is needed to deploy applications to the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="21a11-120">This name is needed to deploy applications to the AKS cluster.</span></span>

```azurecli
$ az aks show --resource-group myResourceGroup --name myAKSCluster --query addonProfiles.httpApplicationRouting.config.HTTPApplicationRoutingZoneName -o table

Result
-----------------------------------------------------
9f9c1fe7-21a1-416d-99cd-3543bb92e4c3.eastus.aksapp.io
```

## <a name="deploy-http-routing-portal"></a><span data-ttu-id="21a11-121">Deploy HTTP routing: Portal</span><span class="sxs-lookup"><span data-stu-id="21a11-121">Deploy HTTP routing: Portal</span></span>

<span data-ttu-id="21a11-122">The HTTP application routing add-on can be enabled through the Azure portal when deploying an AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="21a11-122">The HTTP application routing add-on can be enabled through the Azure portal when deploying an AKS cluster.</span></span>

![Enable the HTTP routing feature](media/http-routing/create.png)

<span data-ttu-id="21a11-124">After the cluster is deployed, browse to the auto-created AKS resource group and select the DNS zone.</span><span class="sxs-lookup"><span data-stu-id="21a11-124">After the cluster is deployed, browse to the auto-created AKS resource group and select the DNS zone.</span></span> <span data-ttu-id="21a11-125">Take note of the DNS zone name.</span><span class="sxs-lookup"><span data-stu-id="21a11-125">Take note of the DNS zone name.</span></span> <span data-ttu-id="21a11-126">This name is needed to deploy applications to the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="21a11-126">This name is needed to deploy applications to the AKS cluster.</span></span>

![Get the DNS zone name](media/http-routing/dns.png)

## <a name="use-http-routing"></a><span data-ttu-id="21a11-128">Use HTTP routing</span><span class="sxs-lookup"><span data-stu-id="21a11-128">Use HTTP routing</span></span>

<span data-ttu-id="21a11-129">The HTTP application routing solution may only be triggered on Ingress resources that are annotated as follows:</span><span class="sxs-lookup"><span data-stu-id="21a11-129">The HTTP application routing solution may only be triggered on Ingress resources that are annotated as follows:</span></span>

```yaml
annotations:
  kubernetes.io/ingress.class: addon-http-application-routing
```

<span data-ttu-id="21a11-130">Create a file named **samples-http-application-routing.yaml** and copy in the following YAML.</span><span class="sxs-lookup"><span data-stu-id="21a11-130">Create a file named **samples-http-application-routing.yaml** and copy in the following YAML.</span></span> <span data-ttu-id="21a11-131">On line 43, update `<CLUSTER_SPECIFIC_DNS_ZONE>` with the DNS zone name collected in the previous step of this article.</span><span class="sxs-lookup"><span data-stu-id="21a11-131">On line 43, update `<CLUSTER_SPECIFIC_DNS_ZONE>` with the DNS zone name collected in the previous step of this article.</span></span>


```yaml
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: party-clippy
spec:
  template:
    metadata:
      labels:
        app: party-clippy
    spec:
      containers:
      - image: r.j3ss.co/party-clippy
        name: party-clippy
        tty: true
        command: ["party-clippy"]
        ports:
        - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  name: party-clippy
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 8080
  selector:
    app: party-clippy
  type: ClusterIP
---
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: party-clippy
  annotations:
    kubernetes.io/ingress.class: addon-http-application-routing
spec:
  rules:
  - host: party-clippy.<CLUSTER_SPECIFIC_DNS_ZONE>
    http:
      paths:
      - backend:
          serviceName: party-clippy
          servicePort: 80
        path: /
```

<span data-ttu-id="21a11-132">Use the [kubectl apply][kubectl-apply] command to create the resources.</span><span class="sxs-lookup"><span data-stu-id="21a11-132">Use the [kubectl apply][kubectl-apply] command to create the resources.</span></span>

```bash
$ kubectl apply -f samples-http-application-routing.yaml

deployment "party-clippy" created
service "party-clippy" created
ingress "party-clippy" created
```

<span data-ttu-id="21a11-133">Use cURL or a browser to navigate to the hostname specified in the host section of the samples-http-application-routing.yaml file.</span><span class="sxs-lookup"><span data-stu-id="21a11-133">Use cURL or a browser to navigate to the hostname specified in the host section of the samples-http-application-routing.yaml file.</span></span> <span data-ttu-id="21a11-134">The application can take up to one minute before it's available via the internet.</span><span class="sxs-lookup"><span data-stu-id="21a11-134">The application can take up to one minute before it's available via the internet.</span></span>

```bash
$ curl party-clippy.471756a6-e744-4aa0-aa01-89c4d162a7a7.canadaeast.aksapp.io

 _________________________________
/ It looks like you're building a \
\ microservice.                   /
 ---------------------------------
 \
  \
     __
    /  \
    |  |
    @  @
    |  |
    || |/
    || ||
    |\_/|
    \___/

```

## <a name="remove-http-routing"></a><span data-ttu-id="21a11-135">Remove HTTP routing</span><span class="sxs-lookup"><span data-stu-id="21a11-135">Remove HTTP routing</span></span>

<span data-ttu-id="21a11-136">The HTTP routing solution can be removed using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="21a11-136">The HTTP routing solution can be removed using the Azure CLI.</span></span> <span data-ttu-id="21a11-137">To do so run the following command, substituting your AKS cluster and resource group name.</span><span class="sxs-lookup"><span data-stu-id="21a11-137">To do so run the following command, substituting your AKS cluster and resource group name.</span></span>

```azurecli
az aks disable-addons --addons http_application_routing --name myAKSCluster --resource-group myResourceGroup --no-wait
```

## <a name="troubleshoot"></a><span data-ttu-id="21a11-138">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="21a11-138">Troubleshoot</span></span>

<span data-ttu-id="21a11-139">Use the [kubectl logs][kubectl-logs] command to view the application logs for the External-DNS application.</span><span class="sxs-lookup"><span data-stu-id="21a11-139">Use the [kubectl logs][kubectl-logs] command to view the application logs for the External-DNS application.</span></span> <span data-ttu-id="21a11-140">The logs should confirm that an A and TXT DNS record were created successfully.</span><span class="sxs-lookup"><span data-stu-id="21a11-140">The logs should confirm that an A and TXT DNS record were created successfully.</span></span>

```
$ kubectl logs -f deploy/addon-http-application-routing-external-dns -n kube-system

time="2018-04-26T20:36:19Z" level=info msg="Updating A record named 'party-clippy' to '52.242.28.189' for Azure DNS zone '471756a6-e744-4aa0-aa01-89c4d162a7a7.canadaeast.aksapp.io'."
time="2018-04-26T20:36:21Z" level=info msg="Updating TXT record named 'party-clippy' to '"heritage=external-dns,external-dns/owner=default"' for Azure DNS zone '471756a6-e744-4aa0-aa01-89c4d162a7a7.canadaeast.aksapp.io'."
```

<span data-ttu-id="21a11-141">These records can also be seen on the DNS zone resource in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="21a11-141">These records can also be seen on the DNS zone resource in the Azure portal.</span></span>

![Get the DNS records](media/http-routing/clippy.png)

<span data-ttu-id="21a11-143">Use the [kubectl logs][kubectl-logs] command to view the application logs for the Nginx Ingress controller.</span><span class="sxs-lookup"><span data-stu-id="21a11-143">Use the [kubectl logs][kubectl-logs] command to view the application logs for the Nginx Ingress controller.</span></span> <span data-ttu-id="21a11-144">The logs should confirm the `CREATE` of an Ingress resource and the reload of the controller.</span><span class="sxs-lookup"><span data-stu-id="21a11-144">The logs should confirm the `CREATE` of an Ingress resource and the reload of the controller.</span></span> <span data-ttu-id="21a11-145">All HTTP activity is logged.</span><span class="sxs-lookup"><span data-stu-id="21a11-145">All HTTP activity is logged.</span></span>

```bash
$ kubectl logs -f deploy/addon-http-application-routing-nginx-ingress-controller -n kube-system

-------------------------------------------------------------------------------
NGINX Ingress controller
  Release:    0.13.0
  Build:      git-4bc943a
  Repository: https://github.com/kubernetes/ingress-nginx
-------------------------------------------------------------------------------

I0426 20:30:12.212936       9 flags.go:162] Watching for ingress class: addon-http-application-routing
W0426 20:30:12.213041       9 flags.go:165] only Ingress with class "addon-http-application-routing" will be processed by this ingress controller
W0426 20:30:12.213505       9 client_config.go:533] Neither --kubeconfig nor --master was specified.  Using the inClusterConfig.  This might not work.
I0426 20:30:12.213752       9 main.go:181] Creating API client for https://10.0.0.1:443
I0426 20:30:12.287928       9 main.go:225] Running in Kubernetes Cluster version v1.8 (v1.8.11) - git (clean) commit 1df6a8381669a6c753f79cb31ca2e3d57ee7c8a3 - platform linux/amd64
I0426 20:30:12.290988       9 main.go:84] validated kube-system/addon-http-application-routing-default-http-backend as the default backend
I0426 20:30:12.294314       9 main.go:105] service kube-system/addon-http-application-routing-nginx-ingress validated as source of Ingress status
I0426 20:30:12.426443       9 stat_collector.go:77] starting new nginx stats collector for Ingress controller running in namespace  (class addon-http-application-routing)
I0426 20:30:12.426509       9 stat_collector.go:78] collector extracting information from port 18080
I0426 20:30:12.448779       9 nginx.go:281] starting Ingress controller
I0426 20:30:12.463585       9 event.go:218] Event(v1.ObjectReference{Kind:"ConfigMap", Namespace:"kube-system", Name:"addon-http-application-routing-nginx-configuration", UID:"2588536c-4990-11e8-a5e1-0a58ac1f0ef2", APIVersion:"v1", ResourceVersion:"559", FieldPath:""}): type: 'Normal' reason: 'CREATE' ConfigMap kube-system/addon-http-application-routing-nginx-configuration
I0426 20:30:12.466945       9 event.go:218] Event(v1.ObjectReference{Kind:"ConfigMap", Namespace:"kube-system", Name:"addon-http-application-routing-tcp-services", UID:"258ca065-4990-11e8-a5e1-0a58ac1f0ef2", APIVersion:"v1", ResourceVersion:"561", FieldPath:""}): type: 'Normal' reason: 'CREATE' ConfigMap kube-system/addon-http-application-routing-tcp-services
I0426 20:30:12.467053       9 event.go:218] Event(v1.ObjectReference{Kind:"ConfigMap", Namespace:"kube-system", Name:"addon-http-application-routing-udp-services", UID:"259023bc-4990-11e8-a5e1-0a58ac1f0ef2", APIVersion:"v1", ResourceVersion:"562", FieldPath:""}): type: 'Normal' reason: 'CREATE' ConfigMap kube-system/addon-http-application-routing-udp-services
I0426 20:30:13.649195       9 nginx.go:302] starting NGINX process...
I0426 20:30:13.649347       9 leaderelection.go:175] attempting to acquire leader lease  kube-system/ingress-controller-leader-addon-http-application-routing...
I0426 20:30:13.649776       9 controller.go:170] backend reload required
I0426 20:30:13.649800       9 stat_collector.go:34] changing prometheus collector from  to default
I0426 20:30:13.662191       9 leaderelection.go:184] successfully acquired lease kube-system/ingress-controller-leader-addon-http-application-routing
I0426 20:30:13.662292       9 status.go:196] new leader elected: addon-http-application-routing-nginx-ingress-controller-5cxntd6
I0426 20:30:13.763362       9 controller.go:179] ingress backend successfully reloaded...
I0426 21:51:55.249327       9 event.go:218] Event(v1.ObjectReference{Kind:"Ingress", Namespace:"default", Name:"party-clippy", UID:"092c9599-499c-11e8-a5e1-0a58ac1f0ef2", APIVersion:"extensions", ResourceVersion:"7346", FieldPath:""}): type: 'Normal' reason: 'CREATE' Ingress default/party-clippy
W0426 21:51:57.908771       9 controller.go:775] service default/party-clippy does not have any active endpoints
I0426 21:51:57.908951       9 controller.go:170] backend reload required
I0426 21:51:58.042932       9 controller.go:179] ingress backend successfully reloaded...
167.220.24.46 - [167.220.24.46] - - [26/Apr/2018:21:53:20 +0000] "GET / HTTP/1.1" 200 234 "" "Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Trident/5.0)" 197 0.001 [default-party-clippy-80] 10.244.0.13:8080 234 0.004 200
```

## <a name="clean-up"></a><span data-ttu-id="21a11-146">Clean up</span><span class="sxs-lookup"><span data-stu-id="21a11-146">Clean up</span></span>

<span data-ttu-id="21a11-147">Remove the associated Kubernetes objects created in this article.</span><span class="sxs-lookup"><span data-stu-id="21a11-147">Remove the associated Kubernetes objects created in this article.</span></span>

```bash
$ kubectl delete -f samples-http-application-routing.yaml

deployment "party-clippy" deleted
service "party-clippy" deleted
ingress "party-clippy" deleted
```

## <a name="next-steps"></a><span data-ttu-id="21a11-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="21a11-148">Next steps</span></span>

<span data-ttu-id="21a11-149">For information on how to install an HTTPS-secured Ingress controller in AKS, see [HTTPS Ingress on Azure Kubernetes Service (AKS)][ingress-https].</span><span class="sxs-lookup"><span data-stu-id="21a11-149">For information on how to install an HTTPS-secured Ingress controller in AKS, see [HTTPS Ingress on Azure Kubernetes Service (AKS)][ingress-https].</span></span>

<!-- LINKS - internal -->
[az-aks-create]: /cli/azure/aks?view=azure-cli-latest#az-aks-create
[az-aks-show]: /cli/azure/aks?view=azure-cli-latest#az-aks-show
[ingress-https]: ./ingress-tls.md
[az-aks-enable-addons]: /cli/azure/aks#az-aks-enable-addons


<!-- LINKS - external -->
[dns-pricing]: https://azure.microsoft.com/pricing/details/dns/
[external-dns]: https://github.com/kubernetes-incubator/external-dns
[kubectl-apply]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[kubectl-logs]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#logs
[ingress]: https://kubernetes.io/docs/concepts/services-networking/ingress/
[ingress-resource]: https://kubernetes.io/docs/concepts/services-networking/ingress/#the-ingress-resource
