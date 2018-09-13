---
title: GPUs on Azure Kubernetes Service (AKS)
description: Use GPUs on Azure Kubernetes Service (AKS)
services: container-service
author: lachie83
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 04/05/2018
ms.author: laevenso
ms.custom: mvc
ms.openlocfilehash: 7fb60f3c440b4804ad8c5e6c013ecfa454358833
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865366"
---
# <a name="using-gpus-on-aks"></a><span data-ttu-id="45052-103">Using GPUs on AKS</span><span class="sxs-lookup"><span data-stu-id="45052-103">Using GPUs on AKS</span></span>

<span data-ttu-id="45052-104">AKS supports the creation of GPU enabled node pools.</span><span class="sxs-lookup"><span data-stu-id="45052-104">AKS supports the creation of GPU enabled node pools.</span></span> <span data-ttu-id="45052-105">Azure currently provides single or multiple GPU enabled VMs.</span><span class="sxs-lookup"><span data-stu-id="45052-105">Azure currently provides single or multiple GPU enabled VMs.</span></span> <span data-ttu-id="45052-106">GPU enabled VMs are designed for compute-intensive, graphics-intensive, and visualization workloads.</span><span class="sxs-lookup"><span data-stu-id="45052-106">GPU enabled VMs are designed for compute-intensive, graphics-intensive, and visualization workloads.</span></span> <span data-ttu-id="45052-107">A list of GPU enabled VMs can be found [here](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-gpu).</span><span class="sxs-lookup"><span data-stu-id="45052-107">A list of GPU enabled VMs can be found [here](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-gpu).</span></span>

## <a name="create-an-aks-cluster"></a><span data-ttu-id="45052-108">Create an AKS cluster</span><span class="sxs-lookup"><span data-stu-id="45052-108">Create an AKS cluster</span></span>

<span data-ttu-id="45052-109">GPUs are typically needed for compute-intensive workloads such as graphics-intensive, and visualization workloads.</span><span class="sxs-lookup"><span data-stu-id="45052-109">GPUs are typically needed for compute-intensive workloads such as graphics-intensive, and visualization workloads.</span></span> <span data-ttu-id="45052-110">Refer to the following [document](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-gpu) to determine the right VM size for your workload.</span><span class="sxs-lookup"><span data-stu-id="45052-110">Refer to the following [document](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-gpu) to determine the right VM size for your workload.</span></span>
<span data-ttu-id="45052-111">We recommend a minimum size of `Standard_NC6` for your Azure Kubernetes Service (AKS) nodes.</span><span class="sxs-lookup"><span data-stu-id="45052-111">We recommend a minimum size of `Standard_NC6` for your Azure Kubernetes Service (AKS) nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="45052-112">GPU enabled VMs contain specialized hardware that is subject to higher pricing and region availability.</span><span class="sxs-lookup"><span data-stu-id="45052-112">GPU enabled VMs contain specialized hardware that is subject to higher pricing and region availability.</span></span> <span data-ttu-id="45052-113">For more information, see the [pricing](https://azure.microsoft.com/pricing/) tool and [region availability](https://azure.microsoft.com/global-infrastructure/services/) site for more information.</span><span class="sxs-lookup"><span data-stu-id="45052-113">For more information, see the [pricing](https://azure.microsoft.com/pricing/) tool and [region availability](https://azure.microsoft.com/global-infrastructure/services/) site for more information.</span></span>


<span data-ttu-id="45052-114">If you need an AKS cluster that meets this minimum recommendation, run the following commands.</span><span class="sxs-lookup"><span data-stu-id="45052-114">If you need an AKS cluster that meets this minimum recommendation, run the following commands.</span></span>

<span data-ttu-id="45052-115">Create a resource group for the cluster.</span><span class="sxs-lookup"><span data-stu-id="45052-115">Create a resource group for the cluster.</span></span>

```azurecli
az group create --name myGPUCluster --location eastus
```

<span data-ttu-id="45052-116">Create the AKS cluster with nodes that are of size `Standard_NC6`.</span><span class="sxs-lookup"><span data-stu-id="45052-116">Create the AKS cluster with nodes that are of size `Standard_NC6`.</span></span>

```azurecli
az aks create --resource-group myGPUCluster --name myGPUCluster --node-vm-size Standard_NC6
```

<span data-ttu-id="45052-117">Connect to the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="45052-117">Connect to the AKS cluster.</span></span>

```azurecli
az aks get-credentials --resource-group myGPUCluster --name myGPUCluster
```

## <a name="confirm-gpus-are-schedulable"></a><span data-ttu-id="45052-118">Confirm GPUs are schedulable</span><span class="sxs-lookup"><span data-stu-id="45052-118">Confirm GPUs are schedulable</span></span>

<span data-ttu-id="45052-119">Run the following commands to confirm the GPUs are schedulable via Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="45052-119">Run the following commands to confirm the GPUs are schedulable via Kubernetes.</span></span>

<span data-ttu-id="45052-120">Get the current list of nodes.</span><span class="sxs-lookup"><span data-stu-id="45052-120">Get the current list of nodes.</span></span>

```
$ kubectl get nodes
NAME                       STATUS    ROLES     AGE       VERSION
aks-nodepool1-22139053-0   Ready     agent     10h       v1.9.6
aks-nodepool1-22139053-1   Ready     agent     10h       v1.9.6
aks-nodepool1-22139053-2   Ready     agent     10h       v1.9.6
```

<span data-ttu-id="45052-121">Describe one of the nodes to confirm the GPUs are schedulable.</span><span class="sxs-lookup"><span data-stu-id="45052-121">Describe one of the nodes to confirm the GPUs are schedulable.</span></span> <span data-ttu-id="45052-122">This can be found under the `Capacity` section.</span><span class="sxs-lookup"><span data-stu-id="45052-122">This can be found under the `Capacity` section.</span></span> <span data-ttu-id="45052-123">For example, `alpha.kubernetes.io/nvidia-gpu:  1`.</span><span class="sxs-lookup"><span data-stu-id="45052-123">For example, `alpha.kubernetes.io/nvidia-gpu:  1`.</span></span>

```
$ kubectl describe node aks-nodepool1-22139053-0
Name:               aks-nodepool1-22139053-0
Roles:              agent
Labels:             agentpool=nodepool1
                    beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/instance-type=Standard_NC6
                    beta.kubernetes.io/os=linux
                    failure-domain.beta.kubernetes.io/region=eastus
                    failure-domain.beta.kubernetes.io/zone=1
                    kubernetes.azure.com/cluster=MC_myGPUCluster_myGPUCluster
                    kubernetes.io/hostname=aks-nodepool1-22139053-0
                    kubernetes.io/role=agent
                    storageprofile=managed
                    storagetier=Standard_LRS
Annotations:        node.alpha.kubernetes.io/ttl=0
                    volumes.kubernetes.io/controller-managed-attach-detach=true
Taints:             <none>
CreationTimestamp:  Thu, 05 Apr 2018 12:13:20 -0700
Conditions:
  Type                 Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----                 ------  -----------------                 ------------------                ------                       -------
  NetworkUnavailable   False   Thu, 05 Apr 2018 12:15:07 -0700   Thu, 05 Apr 2018 12:15:07 -0700   RouteCreated                 RouteController created a route
  OutOfDisk            False   Thu, 05 Apr 2018 22:14:33 -0700   Thu, 05 Apr 2018 12:13:20 -0700   KubeletHasSufficientDisk     kubelet has sufficient disk space available
  MemoryPressure       False   Thu, 05 Apr 2018 22:14:33 -0700   Thu, 05 Apr 2018 12:13:20 -0700   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure         False   Thu, 05 Apr 2018 22:14:33 -0700   Thu, 05 Apr 2018 12:13:20 -0700   KubeletHasNoDiskPressure     kubelet has no disk pressure
  Ready                True    Thu, 05 Apr 2018 22:14:33 -0700   Thu, 05 Apr 2018 12:15:10 -0700   KubeletReady                 kubelet is posting ready status. AppArmor enabled
Addresses:
  InternalIP:  10.240.0.4
  Hostname:    aks-nodepool1-22139053-0
Capacity:
 alpha.kubernetes.io/nvidia-gpu:  1
 cpu:                             6
 memory:                          57691688Ki
 pods:                            110
Allocatable:
 alpha.kubernetes.io/nvidia-gpu:  1
 cpu:                             6
 memory:                          57589288Ki
 pods:                            110
System Info:
 Machine ID:                 2eb0e90bd1fe450ba3cf83479443a511
 System UUID:                CFB485B6-CB49-A545-A2C9-8E4C592C3273
 Boot ID:                    fea24544-596d-4246-b8c3-610fc7ac7280
 Kernel Version:             4.13.0-1011-azure
 OS Image:                   Debian GNU/Linux 9 (stretch)
 Operating System:           linux
 Architecture:               amd64
 Container Runtime Version:  docker://1.13.1
 Kubelet Version:            v1.9.6
 Kube-Proxy Version:         v1.9.6
PodCIDR:                     10.244.1.0/24
ExternalID:                  /subscriptions/8ecadfc9-d1a3-4ea4-b844-0d9f87e4d7c8/resourceGroups/MC_myGPUCluster_myGPUCluster/providers/Microsoft.Compute/virtualMachines/aks-nodepool1-22139053-0
Non-terminated Pods:         (2 in total)
  Namespace                  Name                       CPU Requests  CPU Limits  Memory Requests  Memory Limits
  ---------                  ----                       ------------  ----------  ---------------  -------------
  kube-system                kube-proxy-pwffr           100m (1%)     0 (0%)      0 (0%)           0 (0%)
  kube-system                kube-svc-redirect-mkpf4    0 (0%)        0 (0%)      0 (0%)           0 (0%)
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  CPU Requests  CPU Limits  Memory Requests  Memory Limits
  ------------  ----------  ---------------  -------------
  100m (1%)     0 (0%)      0 (0%)           0 (0%)
Events:         <none>
```

## <a name="run-a-gpu-enabled-workload"></a><span data-ttu-id="45052-124">Run a GPU enabled workload</span><span class="sxs-lookup"><span data-stu-id="45052-124">Run a GPU enabled workload</span></span>

<span data-ttu-id="45052-125">In order to demonstrate the GPUs are indeed working, schedule a GPU enabled workload with the appropriate resource request.</span><span class="sxs-lookup"><span data-stu-id="45052-125">In order to demonstrate the GPUs are indeed working, schedule a GPU enabled workload with the appropriate resource request.</span></span> <span data-ttu-id="45052-126">This example will run a [Tensorflow](https://www.tensorflow.org/versions/r1.1/get_started/mnist/beginners) job against the [MNIST dataset](http://yann.lecun.com/exdb/mnist/).</span><span class="sxs-lookup"><span data-stu-id="45052-126">This example will run a [Tensorflow](https://www.tensorflow.org/versions/r1.1/get_started/mnist/beginners) job against the [MNIST dataset](http://yann.lecun.com/exdb/mnist/).</span></span>

<span data-ttu-id="45052-127">The following job manifest includes a resource limit of `alpha.kubernetes.io/nvidia-gpu: 1`.</span><span class="sxs-lookup"><span data-stu-id="45052-127">The following job manifest includes a resource limit of `alpha.kubernetes.io/nvidia-gpu: 1`.</span></span> <span data-ttu-id="45052-128">The appropriate CUDA libraries and debug tools will be available on the node at `/usr/local/nvidia` and must be mounted into the pod using the appropriate volume specification as seen below.</span><span class="sxs-lookup"><span data-stu-id="45052-128">The appropriate CUDA libraries and debug tools will be available on the node at `/usr/local/nvidia` and must be mounted into the pod using the appropriate volume specification as seen below.</span></span>

<span data-ttu-id="45052-129">Copy the manifest and save as **samples-tf-mnist-demo.yaml**.</span><span class="sxs-lookup"><span data-stu-id="45052-129">Copy the manifest and save as **samples-tf-mnist-demo.yaml**.</span></span>
```
apiVersion: batch/v1
kind: Job
metadata:
  labels:
    app: samples-tf-mnist-demo
  name: samples-tf-mnist-demo
spec:
  template:
    metadata:
      labels:
        app: samples-tf-mnist-demo
    spec:
      containers:
      - name: samples-tf-mnist-demo
        image: microsoft/samples-tf-mnist-demo:gpu
        args: ["--max_steps", "500"]
        imagePullPolicy: IfNotPresent
        resources:
          limits:
            alpha.kubernetes.io/nvidia-gpu: 1
        volumeMounts:
        - name: nvidia
          mountPath: /usr/local/nvidia
      restartPolicy: OnFailure
      volumes:
        - name: nvidia
          hostPath:
            path: /usr/local/nvidia
```

<span data-ttu-id="45052-130">Use the [kubectl apply][kubectl-apply] command to run the job.</span><span class="sxs-lookup"><span data-stu-id="45052-130">Use the [kubectl apply][kubectl-apply] command to run the job.</span></span> <span data-ttu-id="45052-131">This command parses the manifest file and creates the defined Kubernetes objects.</span><span class="sxs-lookup"><span data-stu-id="45052-131">This command parses the manifest file and creates the defined Kubernetes objects.</span></span>
```
$ kubectl apply -f samples-tf-mnist-demo.yaml
job "samples-tf-mnist-demo" created
```

<span data-ttu-id="45052-132">Monitor the progress of the job until successful completion using the [kubectl get jobs][kubectl-get] command with the `--watch` argument.</span><span class="sxs-lookup"><span data-stu-id="45052-132">Monitor the progress of the job until successful completion using the [kubectl get jobs][kubectl-get] command with the `--watch` argument.</span></span>
```
$ kubectl get jobs samples-tf-mnist-demo --watch
NAME                    DESIRED   SUCCESSFUL   AGE
samples-tf-mnist-demo   1         0            8s
samples-tf-mnist-demo   1         1            35s
```

<span data-ttu-id="45052-133">Determine the pod name to view the logs by showing completed pods.</span><span class="sxs-lookup"><span data-stu-id="45052-133">Determine the pod name to view the logs by showing completed pods.</span></span>
```
$ kubectl get pods --selector app=samples-tf-mnist-demo --show-all
NAME                          READY     STATUS      RESTARTS   AGE
samples-tf-mnist-demo-smnr6   0/1       Completed   0          4m
```

<span data-ttu-id="45052-134">Using the pod name from the output of the command above, refer to the pod logs to confirm that the appropriate GPU device has been discovered in this case, `Tesla K80`.</span><span class="sxs-lookup"><span data-stu-id="45052-134">Using the pod name from the output of the command above, refer to the pod logs to confirm that the appropriate GPU device has been discovered in this case, `Tesla K80`.</span></span>
```
$ kubectl logs samples-tf-mnist-demo-smnr6
2018-04-13 04:11:08.710863: I tensorflow/core/platform/cpu_feature_guard.cc:137] Your CPU supports instructions that this TensorFlow binary was not compiled to use: SSE4.1 SSE4.2 AVX AVX2 FMA
2018-04-13 04:11:15.824349: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1030] Found device 0 with properties:
name: Tesla K80 major: 3 minor: 7 memoryClockRate(GHz): 0.8235
pciBusID: 04e1:00:00.0
totalMemory: 11.17GiB freeMemory: 11.10GiB
2018-04-13 04:11:15.824394: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1120] Creating TensorFlow device (/device:GPU:0) -> (device: 0, name: Tesla K80, pci bus id: 04e1:00:00.0, compute capability: 3.7)
2018-04-13 04:11:20.891910: I tensorflow/stream_executor/dso_loader.cc:139] successfully opened CUDA library libcupti.so.8.0 locally
Successfully downloaded train-images-idx3-ubyte.gz 9912422 bytes.
Extracting /tmp/tensorflow/input_data/train-images-idx3-ubyte.gz
Successfully downloaded train-labels-idx1-ubyte.gz 28881 bytes.
Extracting /tmp/tensorflow/input_data/train-labels-idx1-ubyte.gz
Successfully downloaded t10k-images-idx3-ubyte.gz 1648877 bytes.
Extracting /tmp/tensorflow/input_data/t10k-images-idx3-ubyte.gz
Successfully downloaded t10k-labels-idx1-ubyte.gz 4542 bytes.
Extracting /tmp/tensorflow/input_data/t10k-labels-idx1-ubyte.gz
Accuracy at step 0: 0.0487
Accuracy at step 10: 0.6571
Accuracy at step 20: 0.8111
Accuracy at step 30: 0.8562
Accuracy at step 40: 0.8786
Accuracy at step 50: 0.8911
Accuracy at step 60: 0.8986
Accuracy at step 70: 0.9017
Accuracy at step 80: 0.9049
Accuracy at step 90: 0.9114
Adding run metadata for 99
Accuracy at step 100: 0.9109
Accuracy at step 110: 0.9143
Accuracy at step 120: 0.9188
Accuracy at step 130: 0.9194
Accuracy at step 140: 0.9237
Accuracy at step 150: 0.9231
Accuracy at step 160: 0.9158
Accuracy at step 170: 0.9259
Accuracy at step 180: 0.9303
Accuracy at step 190: 0.9315
Adding run metadata for 199
Accuracy at step 200: 0.9334
Accuracy at step 210: 0.9342
Accuracy at step 220: 0.9359
Accuracy at step 230: 0.9353
Accuracy at step 240: 0.933
Accuracy at step 250: 0.9353
Accuracy at step 260: 0.9408
Accuracy at step 270: 0.9396
Accuracy at step 280: 0.9406
Accuracy at step 290: 0.9444
Adding run metadata for 299
Accuracy at step 300: 0.9453
Accuracy at step 310: 0.946
Accuracy at step 320: 0.9464
Accuracy at step 330: 0.9472
Accuracy at step 340: 0.9516
Accuracy at step 350: 0.9473
Accuracy at step 360: 0.9502
Accuracy at step 370: 0.9483
Accuracy at step 380: 0.9481
Accuracy at step 390: 0.9467
Adding run metadata for 399
Accuracy at step 400: 0.9477
Accuracy at step 410: 0.948
Accuracy at step 420: 0.9496
Accuracy at step 430: 0.9501
Accuracy at step 440: 0.9534
Accuracy at step 450: 0.9551
Accuracy at step 460: 0.9518
Accuracy at step 470: 0.9562
Accuracy at step 480: 0.9583
Accuracy at step 490: 0.9575
Adding run metadata for 499
```

## <a name="cleanup"></a><span data-ttu-id="45052-135">Cleanup</span><span class="sxs-lookup"><span data-stu-id="45052-135">Cleanup</span></span>
<span data-ttu-id="45052-136">Remove the associated Kubernetes objects created in this step.</span><span class="sxs-lookup"><span data-stu-id="45052-136">Remove the associated Kubernetes objects created in this step.</span></span>
```
$ kubectl delete jobs samples-tf-mnist-demo
job "samples-tf-mnist-demo" deleted
```

## <a name="troubleshoot"></a><span data-ttu-id="45052-137">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="45052-137">Troubleshoot</span></span>

<span data-ttu-id="45052-138">In some scenarios, you might not see GPU resources under Capacity.</span><span class="sxs-lookup"><span data-stu-id="45052-138">In some scenarios, you might not see GPU resources under Capacity.</span></span> <span data-ttu-id="45052-139">For example: After upgrading a cluster to Kubernetes version 1.10 or creating a new Kubernetes version 1.10 cluster, the expected `nvidia.com/gpu` resource is missing from `Capacity` when running `kubectl describe node <node-name>`.</span><span class="sxs-lookup"><span data-stu-id="45052-139">For example: After upgrading a cluster to Kubernetes version 1.10 or creating a new Kubernetes version 1.10 cluster, the expected `nvidia.com/gpu` resource is missing from `Capacity` when running `kubectl describe node <node-name>`.</span></span> 

<span data-ttu-id="45052-140">To resolve this, apply the following daemonset post provision or upgrade, then you will see `nvidia.com/gpu` as a schedulable resource.</span><span class="sxs-lookup"><span data-stu-id="45052-140">To resolve this, apply the following daemonset post provision or upgrade, then you will see `nvidia.com/gpu` as a schedulable resource.</span></span> 

<span data-ttu-id="45052-141">Copy the manifest and save as **nvidia-device-plugin-ds.yaml**.</span><span class="sxs-lookup"><span data-stu-id="45052-141">Copy the manifest and save as **nvidia-device-plugin-ds.yaml**.</span></span> <span data-ttu-id="45052-142">For the image tag of `image: nvidia/k8s-device-plugin:1.10` below, update the tag to match your Kubernetes version.</span><span class="sxs-lookup"><span data-stu-id="45052-142">For the image tag of `image: nvidia/k8s-device-plugin:1.10` below, update the tag to match your Kubernetes version.</span></span> <span data-ttu-id="45052-143">For example, use tag `1.11` for Kubernetes version 1.11.</span><span class="sxs-lookup"><span data-stu-id="45052-143">For example, use tag `1.11` for Kubernetes version 1.11.</span></span>

```yaml
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
  labels:
    kubernetes.io/cluster-service: "true"
  name: nvidia-device-plugin
  namespace: kube-system
spec:
  template:
    metadata:
      # Mark this pod as a critical add-on; when enabled, the critical add-on scheduler
      # reserves resources for critical add-on pods so that they can be rescheduled after
      # a failure.  This annotation works in tandem with the toleration below.
      annotations:
        scheduler.alpha.kubernetes.io/critical-pod: ""
      labels:
        name: nvidia-device-plugin-ds
    spec:
      tolerations:
      # Allow this pod to be rescheduled while the node is in "critical add-ons only" mode.
      # This, along with the annotation above marks this pod as a critical add-on.
      - key: CriticalAddonsOnly
        operator: Exists
      containers:
      - image: nvidia/k8s-device-plugin:1.10 # Update this tag to match your Kubernetes version
        name: nvidia-device-plugin-ctr
        securityContext:
          allowPrivilegeEscalation: false
          capabilities:
            drop: ["ALL"]
        volumeMounts:
          - name: device-plugin
            mountPath: /var/lib/kubelet/device-plugins
      volumes:
        - name: device-plugin
          hostPath:
            path: /var/lib/kubelet/device-plugins
      nodeSelector:
        beta.kubernetes.io/os: linux
        accelerator: nvidia
```

<span data-ttu-id="45052-144">Use the [kubectl apply][kubectl-apply] command to create the daemonset.</span><span class="sxs-lookup"><span data-stu-id="45052-144">Use the [kubectl apply][kubectl-apply] command to create the daemonset.</span></span>

```
$ kubectl apply -f nvidia-device-plugin-ds.yaml
daemonset "nvidia-device-plugin" created
```

## <a name="next-steps"></a><span data-ttu-id="45052-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="45052-145">Next steps</span></span>

<span data-ttu-id="45052-146">Interested in running Machine Learning workloads on Kubernetes?</span><span class="sxs-lookup"><span data-stu-id="45052-146">Interested in running Machine Learning workloads on Kubernetes?</span></span> <span data-ttu-id="45052-147">Refer to the Kubeflow labs for more detail.</span><span class="sxs-lookup"><span data-stu-id="45052-147">Refer to the Kubeflow labs for more detail.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="45052-148">[Kubeflow Labs][kubeflow-labs]</span><span class="sxs-lookup"><span data-stu-id="45052-148">[Kubeflow Labs][kubeflow-labs]</span></span>

<!-- LINKS - external -->
[kubectl-apply]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[kubeflow-labs]: https://github.com/Azure/kubeflow-labs
