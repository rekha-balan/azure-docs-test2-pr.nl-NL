---
title: Deploy containers with Helm in Kubernetes on Azure
description: Use the Helm packaging tool to deploy containers in an Azure Kubernetes Service (AKS) cluster
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 07/13/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: dd2deba25615373765dd3492d03c1ba547c8ba8c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856271"
---
# <a name="install-applications-with-helm-in-azure-kubernetes-service-aks"></a><span data-ttu-id="266a0-103">Install applications with Helm in Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="266a0-103">Install applications with Helm in Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="266a0-104">[Helm][helm] is an open-source packaging tool that helps you install and manage the lifecycle of Kubernetes applications.</span><span class="sxs-lookup"><span data-stu-id="266a0-104">[Helm][helm] is an open-source packaging tool that helps you install and manage the lifecycle of Kubernetes applications.</span></span> <span data-ttu-id="266a0-105">Similar to Linux package managers such as *APT* and *Yum*, Helm is used to manage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span><span class="sxs-lookup"><span data-stu-id="266a0-105">Similar to Linux package managers such as *APT* and *Yum*, Helm is used to manage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span></span>

<span data-ttu-id="266a0-106">This article shows you how to configure and use Helm in a Kubernetes cluster on AKS.</span><span class="sxs-lookup"><span data-stu-id="266a0-106">This article shows you how to configure and use Helm in a Kubernetes cluster on AKS.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="266a0-107">Before you begin</span><span class="sxs-lookup"><span data-stu-id="266a0-107">Before you begin</span></span>

<span data-ttu-id="266a0-108">The steps detailed in this document assume that you have created an AKS cluster and have established a `kubectl` connection with the cluster.</span><span class="sxs-lookup"><span data-stu-id="266a0-108">The steps detailed in this document assume that you have created an AKS cluster and have established a `kubectl` connection with the cluster.</span></span> <span data-ttu-id="266a0-109">If you need these items see, the [AKS quickstart][aks-quickstart].</span><span class="sxs-lookup"><span data-stu-id="266a0-109">If you need these items see, the [AKS quickstart][aks-quickstart].</span></span>

## <a name="install-helm-cli"></a><span data-ttu-id="266a0-110">Install Helm CLI</span><span class="sxs-lookup"><span data-stu-id="266a0-110">Install Helm CLI</span></span>

<span data-ttu-id="266a0-111">The Helm CLI is a client that runs on your development system and allows you to start, stop, and manage applications with Helm.</span><span class="sxs-lookup"><span data-stu-id="266a0-111">The Helm CLI is a client that runs on your development system and allows you to start, stop, and manage applications with Helm.</span></span>

<span data-ttu-id="266a0-112">If you use the Azure Cloud Shell, the Helm CLI is already installed.</span><span class="sxs-lookup"><span data-stu-id="266a0-112">If you use the Azure Cloud Shell, the Helm CLI is already installed.</span></span> <span data-ttu-id="266a0-113">To install the Helm CLI on a Mac, use `brew`.</span><span class="sxs-lookup"><span data-stu-id="266a0-113">To install the Helm CLI on a Mac, use `brew`.</span></span> <span data-ttu-id="266a0-114">For additional installation options see, [Installing Helm][helm-install-options].</span><span class="sxs-lookup"><span data-stu-id="266a0-114">For additional installation options see, [Installing Helm][helm-install-options].</span></span>

```console
brew install kubernetes-helm
```

<span data-ttu-id="266a0-115">Output:</span><span class="sxs-lookup"><span data-stu-id="266a0-115">Output:</span></span>

```
==> Downloading https://homebrew.bintray.com/bottles/kubernetes-helm-2.9.1.high_sierra.bottle.tar.gz
######################################################################## 100.0%
==> Pouring kubernetes-helm-2.9.1.high_sierra.bottle.tar.gz
==> Caveats
Bash completion has been installed to:
  /usr/local/etc/bash_completion.d
==> Summary
🍺  /usr/local/Cellar/kubernetes-helm/2.9.1: 50 files, 66.2MB
```

## <a name="create-a-service-account"></a><span data-ttu-id="266a0-116">Create a service account</span><span class="sxs-lookup"><span data-stu-id="266a0-116">Create a service account</span></span>

<span data-ttu-id="266a0-117">Before you can deploy Helm in an RBAC-enabled cluster, you need a service account and role binding for the Tiller service.</span><span class="sxs-lookup"><span data-stu-id="266a0-117">Before you can deploy Helm in an RBAC-enabled cluster, you need a service account and role binding for the Tiller service.</span></span> <span data-ttu-id="266a0-118">For more information on securing Helm / Tiller in an RBAC enabled cluster, see [Tiller, Namespaces, and RBAC][tiller-rbac].</span><span class="sxs-lookup"><span data-stu-id="266a0-118">For more information on securing Helm / Tiller in an RBAC enabled cluster, see [Tiller, Namespaces, and RBAC][tiller-rbac].</span></span> <span data-ttu-id="266a0-119">If your cluster is not RBAC enabled, skip this step.</span><span class="sxs-lookup"><span data-stu-id="266a0-119">If your cluster is not RBAC enabled, skip this step.</span></span>

<span data-ttu-id="266a0-120">Create a file named `helm-rbac.yaml` and copy in the following YAML:</span><span class="sxs-lookup"><span data-stu-id="266a0-120">Create a file named `helm-rbac.yaml` and copy in the following YAML:</span></span>

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: tiller
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: tiller
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
  - kind: ServiceAccount
    name: tiller
    namespace: kube-system
```

<span data-ttu-id="266a0-121">Create the service account and role binding with the `kubectl create` command:</span><span class="sxs-lookup"><span data-stu-id="266a0-121">Create the service account and role binding with the `kubectl create` command:</span></span>

```console
kubectl create -f helm-rbac.yaml
```

## <a name="secure-tiller-and-helm"></a><span data-ttu-id="266a0-122">Secure Tiller and Helm</span><span class="sxs-lookup"><span data-stu-id="266a0-122">Secure Tiller and Helm</span></span>

<span data-ttu-id="266a0-123">The Helm client and Tiller service authenticate and communicate with each other using TLS/SSL.</span><span class="sxs-lookup"><span data-stu-id="266a0-123">The Helm client and Tiller service authenticate and communicate with each other using TLS/SSL.</span></span> <span data-ttu-id="266a0-124">This authentication method helps to secure the Kubernetes cluster and what services can be deployed.</span><span class="sxs-lookup"><span data-stu-id="266a0-124">This authentication method helps to secure the Kubernetes cluster and what services can be deployed.</span></span> <span data-ttu-id="266a0-125">To improve security, you can generate your own signed certificates.</span><span class="sxs-lookup"><span data-stu-id="266a0-125">To improve security, you can generate your own signed certificates.</span></span> <span data-ttu-id="266a0-126">Each Helm user would receive their own client certificate, and Tiller would be initialized in the Kubernetes cluster with certificates applied.</span><span class="sxs-lookup"><span data-stu-id="266a0-126">Each Helm user would receive their own client certificate, and Tiller would be initialized in the Kubernetes cluster with certificates applied.</span></span> <span data-ttu-id="266a0-127">For more information, see [Using TLS/SSL between Helm and Tiller][helm-ssl].</span><span class="sxs-lookup"><span data-stu-id="266a0-127">For more information, see [Using TLS/SSL between Helm and Tiller][helm-ssl].</span></span>

<span data-ttu-id="266a0-128">With an RBAC-enabled Kubernetes cluster, you can control the level of access Tiller has to the cluster.</span><span class="sxs-lookup"><span data-stu-id="266a0-128">With an RBAC-enabled Kubernetes cluster, you can control the level of access Tiller has to the cluster.</span></span> <span data-ttu-id="266a0-129">You can define the Kubernetes namespace that Tiller is deployed in, and restrict what namespaces Tiller can then deploy resources in.</span><span class="sxs-lookup"><span data-stu-id="266a0-129">You can define the Kubernetes namespace that Tiller is deployed in, and restrict what namespaces Tiller can then deploy resources in.</span></span> <span data-ttu-id="266a0-130">This approach lets you create Tiller instances in different namespaces and limit deployment boundaries, and scope the users of Helm client to certain namespaces.</span><span class="sxs-lookup"><span data-stu-id="266a0-130">This approach lets you create Tiller instances in different namespaces and limit deployment boundaries, and scope the users of Helm client to certain namespaces.</span></span> <span data-ttu-id="266a0-131">For more information, see [Helm role-based access controls][helm-rbac].</span><span class="sxs-lookup"><span data-stu-id="266a0-131">For more information, see [Helm role-based access controls][helm-rbac].</span></span>

## <a name="configure-helm"></a><span data-ttu-id="266a0-132">Configure Helm</span><span class="sxs-lookup"><span data-stu-id="266a0-132">Configure Helm</span></span>

<span data-ttu-id="266a0-133">To deploy a basic Tiller into an AKS cluster, use the [helm init][helm-init] command.</span><span class="sxs-lookup"><span data-stu-id="266a0-133">To deploy a basic Tiller into an AKS cluster, use the [helm init][helm-init] command.</span></span> <span data-ttu-id="266a0-134">If your cluster is not RBAC enabled, remove the `--service-account` argument and value.</span><span class="sxs-lookup"><span data-stu-id="266a0-134">If your cluster is not RBAC enabled, remove the `--service-account` argument and value.</span></span> <span data-ttu-id="266a0-135">If you configured TLS/SSL for Tiller and Helm, skip this basic initialization step and instead provide the required `--tiller-tls-` as shown in the next example.</span><span class="sxs-lookup"><span data-stu-id="266a0-135">If you configured TLS/SSL for Tiller and Helm, skip this basic initialization step and instead provide the required `--tiller-tls-` as shown in the next example.</span></span>

```console
helm init --service-account tiller
```

<span data-ttu-id="266a0-136">If you configured TLS/SSL between Helm and Tiller provide the `--tiller-tls-` parameters and names of your own certificates, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="266a0-136">If you configured TLS/SSL between Helm and Tiller provide the `--tiller-tls-` parameters and names of your own certificates, as shown in the following example:</span></span>

```console
helm init \
    --tiller-tls \
    --tiller-tls-cert tiller.cert.pem \
    --tiller-tls-key tiller.key.pem \
    --tiller-tls-verify \
    --tls-ca-cert ca.cert.pem \
    --service-account tiller
```

## <a name="find-helm-charts"></a><span data-ttu-id="266a0-137">Find Helm charts</span><span class="sxs-lookup"><span data-stu-id="266a0-137">Find Helm charts</span></span>

<span data-ttu-id="266a0-138">Helm charts are used to deploy applications into a Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="266a0-138">Helm charts are used to deploy applications into a Kubernetes cluster.</span></span> <span data-ttu-id="266a0-139">To search for pre-created Helm charts, use the [helm search][helm-search] command:</span><span class="sxs-lookup"><span data-stu-id="266a0-139">To search for pre-created Helm charts, use the [helm search][helm-search] command:</span></span>

```console
helm search
```

<span data-ttu-id="266a0-140">The following condensed example output shows some of the Helm charts available for use:</span><span class="sxs-lookup"><span data-stu-id="266a0-140">The following condensed example output shows some of the Helm charts available for use:</span></span>

```
$ helm search

NAME                           CHART VERSION    APP VERSION  DESCRIPTION
stable/acs-engine-autoscaler   2.2.0            2.1.1        Scales worker nodes within agent pools
stable/aerospike               0.1.7            v3.14.1.2    A Helm chart for Aerospike in Kubernetes
stable/anchore-engine          0.1.7            0.1.10       Anchore container analysis and policy evaluatio...
stable/apm-server              0.1.0            6.2.4        The server receives data from the Elastic APM a...
stable/ark                     1.0.1            0.8.2        A Helm chart for ark
stable/artifactory             7.2.1            6.0.0        Universal Repository Manager supporting all maj...
stable/artifactory-ha          0.2.1            6.0.0        Universal Repository Manager supporting all maj...
stable/auditbeat               0.1.0            6.2.4        A lightweight shipper to audit the activities o...
stable/aws-cluster-autoscaler  0.3.3                         Scales worker nodes within autoscaling groups.
stable/bitcoind                0.1.3            0.15.1       Bitcoin is an innovative payment network and a ...
stable/buildkite               0.2.3            3            Agent for Buildkite
stable/burrow                  0.4.4            0.17.1       Burrow is a permissionable smart contract machine
stable/centrifugo              2.0.1            1.7.3        Centrifugo is a real-time messaging server.
stable/cerebro                 0.1.0            0.7.3        A Helm chart for Cerebro - a web admin tool tha...
stable/cert-manager            v0.3.3           v0.3.1       A Helm chart for cert-manager
stable/chaoskube               0.7.0            0.8.0        Chaoskube periodically kills random pods in you...
stable/chartmuseum             1.5.0            0.7.0        Helm Chart Repository with support for Amazon S...
stable/chronograf              0.4.5            1.3          Open-source web application written in Go and R...
stable/cluster-autoscaler      0.6.4            1.2.2        Scales worker nodes within autoscaling groups.
stable/cockroachdb             1.1.1            2.0.0        CockroachDB is a scalable, survivable, strongly...
stable/concourse               1.10.1           3.14.1       Concourse is a simple and scalable CI system.
stable/consul                  3.2.0            1.0.0        Highly available and distributed service discov...
stable/coredns                 0.9.0            1.0.6        CoreDNS is a DNS server that chains plugins and...
stable/coscale                 0.2.1            3.9.1        CoScale Agent
stable/dask                    1.0.4            0.17.4       Distributed computation in Python with task sch...
stable/dask-distributed        2.0.2                         DEPRECATED: Distributed computation in Python
stable/datadog                 0.18.0           6.3.0        DataDog Agent
...
```

<span data-ttu-id="266a0-141">To update the list of charts, use the [helm repo update][helm-repo-update] command.</span><span class="sxs-lookup"><span data-stu-id="266a0-141">To update the list of charts, use the [helm repo update][helm-repo-update] command.</span></span> <span data-ttu-id="266a0-142">The following example shows a successful repo update:</span><span class="sxs-lookup"><span data-stu-id="266a0-142">The following example shows a successful repo update:</span></span>

```console
$ helm repo update

Hang tight while we grab the latest from your chart repositories...
...Skip local chart repository
...Successfully got an update from the "stable" chart repository
Update Complete. ⎈ Happy Helming!⎈
```

## <a name="run-helm-charts"></a><span data-ttu-id="266a0-143">Run Helm charts</span><span class="sxs-lookup"><span data-stu-id="266a0-143">Run Helm charts</span></span>

<span data-ttu-id="266a0-144">To install charts with Helm, use the [helm install][helm-install] command and specify the name of the chart to install.</span><span class="sxs-lookup"><span data-stu-id="266a0-144">To install charts with Helm, use the [helm install][helm-install] command and specify the name of the chart to install.</span></span> <span data-ttu-id="266a0-145">To see this in action, let's install a basic Wordpress deployment using a Helm chart.</span><span class="sxs-lookup"><span data-stu-id="266a0-145">To see this in action, let's install a basic Wordpress deployment using a Helm chart.</span></span> <span data-ttu-id="266a0-146">If you configured TLS/SSL, add the `--tls` parameter to use your Helm client certificate.</span><span class="sxs-lookup"><span data-stu-id="266a0-146">If you configured TLS/SSL, add the `--tls` parameter to use your Helm client certificate.</span></span>

```console
helm install stable/wordpress
```

<span data-ttu-id="266a0-147">The following condensed example output shows the deployment status of the Kubernetes resources created by the Helm chart:</span><span class="sxs-lookup"><span data-stu-id="266a0-147">The following condensed example output shows the deployment status of the Kubernetes resources created by the Helm chart:</span></span>

```
$ helm install stable/wordpress

NAME:   wishful-mastiff
LAST DEPLOYED: Thu Jul 12 15:53:56 2018
NAMESPACE: default
STATUS: DEPLOYED

RESOURCES:
==> v1beta1/Deployment
NAME                       DESIRED  CURRENT  UP-TO-DATE  AVAILABLE  AGE
wishful-mastiff-wordpress  1        1        1           0          1s

==> v1beta1/StatefulSet
NAME                     DESIRED  CURRENT  AGE
wishful-mastiff-mariadb  1        1        1s

==> v1/Pod(related)
NAME                                        READY  STATUS   RESTARTS  AGE
wishful-mastiff-wordpress-6f96f8fdf9-q84sz  0/1    Pending  0         1s
wishful-mastiff-mariadb-0                   0/1    Pending  0         1s

==> v1/Secret
NAME                       TYPE    DATA  AGE
wishful-mastiff-mariadb    Opaque  2     2s
wishful-mastiff-wordpress  Opaque  2     2s

==> v1/ConfigMap
NAME                           DATA  AGE
wishful-mastiff-mariadb        1     2s
wishful-mastiff-mariadb-tests  1     2s

==> v1/PersistentVolumeClaim
NAME                       STATUS   VOLUME   CAPACITY  ACCESS MODES  STORAGECLASS  AGE
wishful-mastiff-wordpress  Pending  default  2s

==> v1/Service
NAME                       TYPE          CLUSTER-IP   EXTERNAL-IP  PORT(S)                     AGE
wishful-mastiff-mariadb    ClusterIP     10.1.116.54  <none>       3306/TCP                    2s
wishful-mastiff-wordpress  LoadBalancer  10.1.217.64  <pending>    80:31751/TCP,443:31264/TCP  2s
...
```

<span data-ttu-id="266a0-148">It takes a minute or two for the *EXTERNAL-IP* address of the Wordpress service to be populated and allow you to access it with a web browser.</span><span class="sxs-lookup"><span data-stu-id="266a0-148">It takes a minute or two for the *EXTERNAL-IP* address of the Wordpress service to be populated and allow you to access it with a web browser.</span></span>

## <a name="list-helm-releases"></a><span data-ttu-id="266a0-149">List Helm releases</span><span class="sxs-lookup"><span data-stu-id="266a0-149">List Helm releases</span></span>

<span data-ttu-id="266a0-150">To see a list of releases installed on your cluster, use the [helm list][helm-list] command.</span><span class="sxs-lookup"><span data-stu-id="266a0-150">To see a list of releases installed on your cluster, use the [helm list][helm-list] command.</span></span> <span data-ttu-id="266a0-151">The following example shows the Wordpress release deployed in the previous step.</span><span class="sxs-lookup"><span data-stu-id="266a0-151">The following example shows the Wordpress release deployed in the previous step.</span></span> <span data-ttu-id="266a0-152">If you configured TLS/SSL, add the `--tls` parameter to use your Helm client certificate.</span><span class="sxs-lookup"><span data-stu-id="266a0-152">If you configured TLS/SSL, add the `--tls` parameter to use your Helm client certificate.</span></span>

```console
$ helm list

NAME             REVISION    UPDATED                     STATUS      CHART              NAMESPACE
wishful-mastiff  1           Thu Jul 12 15:53:56 2018    DEPLOYED    wordpress-2.1.3  default
```

## <a name="next-steps"></a><span data-ttu-id="266a0-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="266a0-153">Next steps</span></span>

<span data-ttu-id="266a0-154">For more information about managing Kubernetes application deployments with Helm, see the Helm documentation.</span><span class="sxs-lookup"><span data-stu-id="266a0-154">For more information about managing Kubernetes application deployments with Helm, see the Helm documentation.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="266a0-155">[Helm documentation][helm-documentation]</span><span class="sxs-lookup"><span data-stu-id="266a0-155">[Helm documentation][helm-documentation]</span></span>

<!-- LINKS - external -->
[helm]: https://github.com/kubernetes/helm/
[helm-documentation]: https://docs.helm.sh/
[helm-init]: https://docs.helm.sh/helm/#helm-init
[helm-install]: https://docs.helm.sh/helm/#helm-install
[helm-install-options]: https://github.com/kubernetes/helm/blob/master/docs/install.md
[helm-list]: https://docs.helm.sh/helm/#helm-list
[helm-rbac]: https://docs.helm.sh/using_helm/#role-based-access-control
[helm-repo-update]: https://docs.helm.sh/helm/#helm-repo-update
[helm-search]: https://docs.helm.sh/helm/#helm-search
[tiller-rbac]: https://docs.helm.sh/using_helm/#tiller-namespaces-and-rbac
[helm-ssl]: https://docs.helm.sh/using_helm/#using-ssl-between-helm-and-tiller

<!-- LINKS - internal -->
[aks-quickstart]: ./kubernetes-walkthrough.md
