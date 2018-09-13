---
title: Run an Apache Spark job with Azure Kubernetes Service (AKS)
description: Use Azure Kubernetes Service (AKS) to run an Apache Spark job
services: container-service
author: lenadroid
manager: jeconnoc
ms.service: container-service
ms.topic: article
ms.date: 03/15/2018
ms.author: alehall
ms.custom: mvc
ms.openlocfilehash: cb23c21fd22a35a3e8a5920a94aa5a89fe966cfa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870878"
---
# <a name="running-apache-spark-jobs-on-aks"></a><span data-ttu-id="964ea-103">Running Apache Spark jobs on AKS</span><span class="sxs-lookup"><span data-stu-id="964ea-103">Running Apache Spark jobs on AKS</span></span>

<span data-ttu-id="964ea-104">[Apache Spark][apache-spark] is a fast engine for large-scale data processing.</span><span class="sxs-lookup"><span data-stu-id="964ea-104">[Apache Spark][apache-spark] is a fast engine for large-scale data processing.</span></span> <span data-ttu-id="964ea-105">As of the [Spark 2.3.0 release][spark-latest-release], Apache Spark supports native integration with Kubernetes clusters.</span><span class="sxs-lookup"><span data-stu-id="964ea-105">As of the [Spark 2.3.0 release][spark-latest-release], Apache Spark supports native integration with Kubernetes clusters.</span></span> <span data-ttu-id="964ea-106">Azure Kubernetes Service (AKS) is a managed Kubernetes environment running in Azure.</span><span class="sxs-lookup"><span data-stu-id="964ea-106">Azure Kubernetes Service (AKS) is a managed Kubernetes environment running in Azure.</span></span> <span data-ttu-id="964ea-107">This document details preparing and running Apache Spark jobs on an Azure Kubernetes Service (AKS) cluster.</span><span class="sxs-lookup"><span data-stu-id="964ea-107">This document details preparing and running Apache Spark jobs on an Azure Kubernetes Service (AKS) cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="964ea-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="964ea-108">Prerequisites</span></span>

<span data-ttu-id="964ea-109">In order to complete the steps within this article, you need the following.</span><span class="sxs-lookup"><span data-stu-id="964ea-109">In order to complete the steps within this article, you need the following.</span></span>

* <span data-ttu-id="964ea-110">Basic understanding of Kubernetes and [Apache Spark][spark-quickstart].</span><span class="sxs-lookup"><span data-stu-id="964ea-110">Basic understanding of Kubernetes and [Apache Spark][spark-quickstart].</span></span>
* <span data-ttu-id="964ea-111">[Docker Hub][docker-hub] account, or an [Azure Container Registry][acr-create].</span><span class="sxs-lookup"><span data-stu-id="964ea-111">[Docker Hub][docker-hub] account, or an [Azure Container Registry][acr-create].</span></span>
* <span data-ttu-id="964ea-112">Azure CLI [installed][azure-cli] on your development system.</span><span class="sxs-lookup"><span data-stu-id="964ea-112">Azure CLI [installed][azure-cli] on your development system.</span></span>
* <span data-ttu-id="964ea-113">[JDK 8][java-install] installed on your system.</span><span class="sxs-lookup"><span data-stu-id="964ea-113">[JDK 8][java-install] installed on your system.</span></span>
* <span data-ttu-id="964ea-114">SBT ([Scala Build Tool][sbt-install]) installed on your system.</span><span class="sxs-lookup"><span data-stu-id="964ea-114">SBT ([Scala Build Tool][sbt-install]) installed on your system.</span></span>
* <span data-ttu-id="964ea-115">Git command-line tools installed on your system.</span><span class="sxs-lookup"><span data-stu-id="964ea-115">Git command-line tools installed on your system.</span></span>

## <a name="create-an-aks-cluster"></a><span data-ttu-id="964ea-116">Create an AKS cluster</span><span class="sxs-lookup"><span data-stu-id="964ea-116">Create an AKS cluster</span></span>

<span data-ttu-id="964ea-117">Spark is used for large-scale data processing and requires that Kubernetes nodes are sized to meet the Spark resources requirements.</span><span class="sxs-lookup"><span data-stu-id="964ea-117">Spark is used for large-scale data processing and requires that Kubernetes nodes are sized to meet the Spark resources requirements.</span></span> <span data-ttu-id="964ea-118">We recommend a minimum size of `Standard_D3_v2` for your Azure Kubernetes Service (AKS) nodes.</span><span class="sxs-lookup"><span data-stu-id="964ea-118">We recommend a minimum size of `Standard_D3_v2` for your Azure Kubernetes Service (AKS) nodes.</span></span>

<span data-ttu-id="964ea-119">If you need an AKS cluster that meets this minimum recommendation, run the following commands.</span><span class="sxs-lookup"><span data-stu-id="964ea-119">If you need an AKS cluster that meets this minimum recommendation, run the following commands.</span></span>

<span data-ttu-id="964ea-120">Create a resource group for the cluster.</span><span class="sxs-lookup"><span data-stu-id="964ea-120">Create a resource group for the cluster.</span></span>

```azurecli
az group create --name mySparkCluster --location eastus
```

<span data-ttu-id="964ea-121">Create the AKS cluster with nodes that are of size `Standard_D3_v2`.</span><span class="sxs-lookup"><span data-stu-id="964ea-121">Create the AKS cluster with nodes that are of size `Standard_D3_v2`.</span></span>

```azurecli
az aks create --resource-group mySparkCluster --name mySparkCluster --node-vm-size Standard_D3_v2
```

<span data-ttu-id="964ea-122">Connect to the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="964ea-122">Connect to the AKS cluster.</span></span>

```azurecli
az aks get-credentials --resource-group mySparkCluster --name mySparkCluster
```

<span data-ttu-id="964ea-123">If you are using Azure Container Registry (ACR) to store container images, configure authentication between AKS and ACR.</span><span class="sxs-lookup"><span data-stu-id="964ea-123">If you are using Azure Container Registry (ACR) to store container images, configure authentication between AKS and ACR.</span></span> <span data-ttu-id="964ea-124">See the [ACR authentication documentation][acr-aks] for these steps.</span><span class="sxs-lookup"><span data-stu-id="964ea-124">See the [ACR authentication documentation][acr-aks] for these steps.</span></span>

## <a name="build-the-spark-source"></a><span data-ttu-id="964ea-125">Build the Spark source</span><span class="sxs-lookup"><span data-stu-id="964ea-125">Build the Spark source</span></span>

<span data-ttu-id="964ea-126">Before running Spark jobs on an AKS cluster, you need to build the Spark source code and package it into a container image.</span><span class="sxs-lookup"><span data-stu-id="964ea-126">Before running Spark jobs on an AKS cluster, you need to build the Spark source code and package it into a container image.</span></span> <span data-ttu-id="964ea-127">The Spark source includes scripts that can be used to complete this process.</span><span class="sxs-lookup"><span data-stu-id="964ea-127">The Spark source includes scripts that can be used to complete this process.</span></span>

<span data-ttu-id="964ea-128">Clone the Spark project repository to your development system.</span><span class="sxs-lookup"><span data-stu-id="964ea-128">Clone the Spark project repository to your development system.</span></span>

```bash
git clone -b branch-2.3 https://github.com/apache/spark
```

<span data-ttu-id="964ea-129">Change into the directory of the cloned repository and save the path of the Spark source to a variable.</span><span class="sxs-lookup"><span data-stu-id="964ea-129">Change into the directory of the cloned repository and save the path of the Spark source to a variable.</span></span>

```bash
cd spark
sparkdir=$(pwd)
```

<span data-ttu-id="964ea-130">If you have multiple JDK versions installed, set `JAVA_HOME` to use version 8 for the current session.</span><span class="sxs-lookup"><span data-stu-id="964ea-130">If you have multiple JDK versions installed, set `JAVA_HOME` to use version 8 for the current session.</span></span>

```bash
export JAVA_HOME=`/usr/libexec/java_home -d 64 -v "1.8*"`
```

<span data-ttu-id="964ea-131">Run the following command to build the Spark source code with Kubernetes support.</span><span class="sxs-lookup"><span data-stu-id="964ea-131">Run the following command to build the Spark source code with Kubernetes support.</span></span>

```bash
./build/mvn -Pkubernetes -DskipTests clean package
```

<span data-ttu-id="964ea-132">The following commands create the Spark container image and push it to a container image registry.</span><span class="sxs-lookup"><span data-stu-id="964ea-132">The following commands create the Spark container image and push it to a container image registry.</span></span> <span data-ttu-id="964ea-133">Replace `registry.example.com` with the name of your container registry and `v1` with the tag you prefer to use.</span><span class="sxs-lookup"><span data-stu-id="964ea-133">Replace `registry.example.com` with the name of your container registry and `v1` with the tag you prefer to use.</span></span> <span data-ttu-id="964ea-134">If using Docker Hub, this value is the registry name.</span><span class="sxs-lookup"><span data-stu-id="964ea-134">If using Docker Hub, this value is the registry name.</span></span> <span data-ttu-id="964ea-135">If using Azure Container Registry (ACR), this value is the ACR login server name.</span><span class="sxs-lookup"><span data-stu-id="964ea-135">If using Azure Container Registry (ACR), this value is the ACR login server name.</span></span>

```bash
REGISTRY_NAME=registry.example.com
REGISTRY_TAG=v1
```

```bash
./bin/docker-image-tool.sh -r $REGISTRY_NAME -t $REGISTRY_TAG build
```

<span data-ttu-id="964ea-136">Push the container image to your container image registry.</span><span class="sxs-lookup"><span data-stu-id="964ea-136">Push the container image to your container image registry.</span></span>

```bash
./bin/docker-image-tool.sh -r $REGISTRY_NAME -t $REGISTRY_TAG push
```

## <a name="prepare-a-spark-job"></a><span data-ttu-id="964ea-137">Prepare a Spark job</span><span class="sxs-lookup"><span data-stu-id="964ea-137">Prepare a Spark job</span></span>

<span data-ttu-id="964ea-138">Next, prepare a Spark job.</span><span class="sxs-lookup"><span data-stu-id="964ea-138">Next, prepare a Spark job.</span></span> <span data-ttu-id="964ea-139">A jar file is used to hold the Spark job and is needed when running the `spark-submit` command.</span><span class="sxs-lookup"><span data-stu-id="964ea-139">A jar file is used to hold the Spark job and is needed when running the `spark-submit` command.</span></span> <span data-ttu-id="964ea-140">The jar can be made accessible through a public URL or pre-packaged within a container image.</span><span class="sxs-lookup"><span data-stu-id="964ea-140">The jar can be made accessible through a public URL or pre-packaged within a container image.</span></span> <span data-ttu-id="964ea-141">In this example, a sample jar is created to calculate the value of Pi.</span><span class="sxs-lookup"><span data-stu-id="964ea-141">In this example, a sample jar is created to calculate the value of Pi.</span></span> <span data-ttu-id="964ea-142">This jar is then uploaded to Azure storage.</span><span class="sxs-lookup"><span data-stu-id="964ea-142">This jar is then uploaded to Azure storage.</span></span> <span data-ttu-id="964ea-143">If you have an existing jar, feel free to substitute</span><span class="sxs-lookup"><span data-stu-id="964ea-143">If you have an existing jar, feel free to substitute</span></span>

<span data-ttu-id="964ea-144">Create a directory where you would like to create the project for a Spark job.</span><span class="sxs-lookup"><span data-stu-id="964ea-144">Create a directory where you would like to create the project for a Spark job.</span></span>

```bash
mkdir myprojects
cd myprojects
```

<span data-ttu-id="964ea-145">Create a new Scala project from a template.</span><span class="sxs-lookup"><span data-stu-id="964ea-145">Create a new Scala project from a template.</span></span>

```bash
sbt new sbt/scala-seed.g8
```

<span data-ttu-id="964ea-146">When prompted, enter `SparkPi` for the project name.</span><span class="sxs-lookup"><span data-stu-id="964ea-146">When prompted, enter `SparkPi` for the project name.</span></span>

```bash
name [Scala Seed Project]: SparkPi
```

<span data-ttu-id="964ea-147">Navigate to the newly created project directory.</span><span class="sxs-lookup"><span data-stu-id="964ea-147">Navigate to the newly created project directory.</span></span>

```bash
cd sparkpi
```

<span data-ttu-id="964ea-148">Run the following commands to add an SBT plugin, which allows packaging the project as a jar file.</span><span class="sxs-lookup"><span data-stu-id="964ea-148">Run the following commands to add an SBT plugin, which allows packaging the project as a jar file.</span></span>

```bash
touch project/assembly.sbt
echo 'addSbtPlugin("com.eed3si9n" % "sbt-assembly" % "0.14.6")' >> project/assembly.sbt
```

<span data-ttu-id="964ea-149">Run these commands to copy the sample code into the newly created project and add all necessary dependencies.</span><span class="sxs-lookup"><span data-stu-id="964ea-149">Run these commands to copy the sample code into the newly created project and add all necessary dependencies.</span></span>

```bash
EXAMPLESDIR="src/main/scala/org/apache/spark/examples"
mkdir -p $EXAMPLESDIR
cp $sparkdir/examples/$EXAMPLESDIR/SparkPi.scala $EXAMPLESDIR/SparkPi.scala

cat <<EOT >> build.sbt
// https://mvnrepository.com/artifact/org.apache.spark/spark-sql
libraryDependencies += "org.apache.spark" %% "spark-sql" % "2.3.0" % "provided"
EOT

sed -ie 's/scalaVersion.*/scalaVersion := "2.11.11",/' build.sbt
sed -ie 's/name.*/name := "SparkPi",/' build.sbt
```

<span data-ttu-id="964ea-150">To package the project into a jar, run the following command.</span><span class="sxs-lookup"><span data-stu-id="964ea-150">To package the project into a jar, run the following command.</span></span>

```bash
sbt assembly
```

<span data-ttu-id="964ea-151">After successful packaging, you should see output similar to the following.</span><span class="sxs-lookup"><span data-stu-id="964ea-151">After successful packaging, you should see output similar to the following.</span></span>

```bash
[info] Packaging /Users/me/myprojects/sparkpi/target/scala-2.11/SparkPi-assembly-0.1.0-SNAPSHOT.jar ...
[info] Done packaging.
[success] Total time: 10 s, completed Mar 6, 2018 11:07:54 AM
```

## <a name="copy-job-to-storage"></a><span data-ttu-id="964ea-152">Copy job to storage</span><span class="sxs-lookup"><span data-stu-id="964ea-152">Copy job to storage</span></span>

<span data-ttu-id="964ea-153">Create an Azure storage account and container to hold the jar file.</span><span class="sxs-lookup"><span data-stu-id="964ea-153">Create an Azure storage account and container to hold the jar file.</span></span>

```azurecli
RESOURCE_GROUP=sparkdemo
STORAGE_ACCT=sparkdemo$RANDOM
az group create --name $RESOURCE_GROUP --location eastus
az storage account create --resource-group $RESOURCE_GROUP --name $STORAGE_ACCT --sku Standard_LRS
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string --resource-group $RESOURCE_GROUP --name $STORAGE_ACCT -o tsv`
```

<span data-ttu-id="964ea-154">Upload the jar file to the Azure storage account with the following commands.</span><span class="sxs-lookup"><span data-stu-id="964ea-154">Upload the jar file to the Azure storage account with the following commands.</span></span>

```bash
CONTAINER_NAME=jars
BLOB_NAME=SparkPi-assembly-0.1.0-SNAPSHOT.jar
FILE_TO_UPLOAD=target/scala-2.11/SparkPi-assembly-0.1.0-SNAPSHOT.jar

echo "Creating the container..."
az storage container create --name $CONTAINER_NAME
az storage container set-permission --name $CONTAINER_NAME --public-access blob

echo "Uploading the file..."
az storage blob upload --container-name $CONTAINER_NAME --file $FILE_TO_UPLOAD --name $BLOB_NAME

jarUrl=$(az storage blob url --container-name $CONTAINER_NAME --name $BLOB_NAME | tr -d '"')
```

<span data-ttu-id="964ea-155">Variable `jarUrl` now contains the publicly accessible path to the jar file.</span><span class="sxs-lookup"><span data-stu-id="964ea-155">Variable `jarUrl` now contains the publicly accessible path to the jar file.</span></span>

## <a name="submit-a-spark-job"></a><span data-ttu-id="964ea-156">Submit a Spark job</span><span class="sxs-lookup"><span data-stu-id="964ea-156">Submit a Spark job</span></span>

<span data-ttu-id="964ea-157">Start kube-proxy in a separate command-line with the following code.</span><span class="sxs-lookup"><span data-stu-id="964ea-157">Start kube-proxy in a separate command-line with the following code.</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="964ea-158">Navigate back to the root of Spark repository.</span><span class="sxs-lookup"><span data-stu-id="964ea-158">Navigate back to the root of Spark repository.</span></span>

```bash
cd $sparkdir
```

<span data-ttu-id="964ea-159">Submit the job using `spark-submit`.</span><span class="sxs-lookup"><span data-stu-id="964ea-159">Submit the job using `spark-submit`.</span></span>

```bash
./bin/spark-submit \
  --master k8s://http://127.0.0.1:8001 \
  --deploy-mode cluster \
  --name spark-pi \
  --class org.apache.spark.examples.SparkPi \
  --conf spark.executor.instances=3 \
  --conf spark.kubernetes.container.image=$REGISTRY_NAME/spark:$REGISTRY_TAG \
  $jarUrl
```

<span data-ttu-id="964ea-160">This operation starts the Spark job, which streams job status to your shell session.</span><span class="sxs-lookup"><span data-stu-id="964ea-160">This operation starts the Spark job, which streams job status to your shell session.</span></span> <span data-ttu-id="964ea-161">While the job is running, you can see Spark driver pod and executor pods using the kubectl get pods command.</span><span class="sxs-lookup"><span data-stu-id="964ea-161">While the job is running, you can see Spark driver pod and executor pods using the kubectl get pods command.</span></span> <span data-ttu-id="964ea-162">Open a second terminal session to run these commands.</span><span class="sxs-lookup"><span data-stu-id="964ea-162">Open a second terminal session to run these commands.</span></span>

```console
$ kubectl get pods

NAME                                               READY     STATUS     RESTARTS   AGE
spark-pi-2232778d0f663768ab27edc35cb73040-driver   1/1       Running    0          16s
spark-pi-2232778d0f663768ab27edc35cb73040-exec-1   0/1       Init:0/1   0          4s
spark-pi-2232778d0f663768ab27edc35cb73040-exec-2   0/1       Init:0/1   0          4s
spark-pi-2232778d0f663768ab27edc35cb73040-exec-3   0/1       Init:0/1   0          4s
```

<span data-ttu-id="964ea-163">While the job is running, you can also access the Spark UI.</span><span class="sxs-lookup"><span data-stu-id="964ea-163">While the job is running, you can also access the Spark UI.</span></span> <span data-ttu-id="964ea-164">In the second terminal session, use the `kubectl port-forward` command provide access to Spark UI.</span><span class="sxs-lookup"><span data-stu-id="964ea-164">In the second terminal session, use the `kubectl port-forward` command provide access to Spark UI.</span></span>

```bash
kubectl port-forward spark-pi-2232778d0f663768ab27edc35cb73040-driver 4040:4040
```

<span data-ttu-id="964ea-165">To access Spark UI, open the address `127.0.0.1:4040` in a browser.</span><span class="sxs-lookup"><span data-stu-id="964ea-165">To access Spark UI, open the address `127.0.0.1:4040` in a browser.</span></span>

![Spark UI](media/aks-spark-job/spark-ui.png)

## <a name="get-job-results-and-logs"></a><span data-ttu-id="964ea-167">Get job results and logs</span><span class="sxs-lookup"><span data-stu-id="964ea-167">Get job results and logs</span></span>

<span data-ttu-id="964ea-168">After the job has finished, the driver pod will be in a "Completed" state.</span><span class="sxs-lookup"><span data-stu-id="964ea-168">After the job has finished, the driver pod will be in a "Completed" state.</span></span> <span data-ttu-id="964ea-169">Get the name of the pod with the following command.</span><span class="sxs-lookup"><span data-stu-id="964ea-169">Get the name of the pod with the following command.</span></span>

```bash
kubectl get pods --show-all
```

<span data-ttu-id="964ea-170">Output:</span><span class="sxs-lookup"><span data-stu-id="964ea-170">Output:</span></span>

```bash
NAME                                               READY     STATUS      RESTARTS   AGE
spark-pi-2232778d0f663768ab27edc35cb73040-driver   0/1       Completed   0          1m
```

<span data-ttu-id="964ea-171">Use the `kubectl logs` command to get logs from the spark driver pod.</span><span class="sxs-lookup"><span data-stu-id="964ea-171">Use the `kubectl logs` command to get logs from the spark driver pod.</span></span> <span data-ttu-id="964ea-172">Replace the pod name with your driver pod's name.</span><span class="sxs-lookup"><span data-stu-id="964ea-172">Replace the pod name with your driver pod's name.</span></span>

```bash
kubectl logs spark-pi-2232778d0f663768ab27edc35cb73040-driver
```

<span data-ttu-id="964ea-173">Within these logs, you can see the result of the Spark job, which is the value of Pi.</span><span class="sxs-lookup"><span data-stu-id="964ea-173">Within these logs, you can see the result of the Spark job, which is the value of Pi.</span></span>

```bash
Pi is roughly 3.152155760778804
```

## <a name="package-jar-with-container-image"></a><span data-ttu-id="964ea-174">Package jar with container image</span><span class="sxs-lookup"><span data-stu-id="964ea-174">Package jar with container image</span></span>

<span data-ttu-id="964ea-175">In the above example, the Spark jar file was uploaded to Azure storage.</span><span class="sxs-lookup"><span data-stu-id="964ea-175">In the above example, the Spark jar file was uploaded to Azure storage.</span></span> <span data-ttu-id="964ea-176">Another option is to package the jar file into custom-built Docker images.</span><span class="sxs-lookup"><span data-stu-id="964ea-176">Another option is to package the jar file into custom-built Docker images.</span></span>

<span data-ttu-id="964ea-177">To do so, find the `dockerfile` for the Spark image located at `$sparkdir/resource-managers/kubernetes/docker/src/main/dockerfiles/spark/` directory.</span><span class="sxs-lookup"><span data-stu-id="964ea-177">To do so, find the `dockerfile` for the Spark image located at `$sparkdir/resource-managers/kubernetes/docker/src/main/dockerfiles/spark/` directory.</span></span> <span data-ttu-id="964ea-178">Add am `ADD` statement for the Spark job `jar` somewhere between `WORKDIR` and `ENTRYPOINT` declarations.</span><span class="sxs-lookup"><span data-stu-id="964ea-178">Add am `ADD` statement for the Spark job `jar` somewhere between `WORKDIR` and `ENTRYPOINT` declarations.</span></span>

<span data-ttu-id="964ea-179">Update the jar path to the location of the `SparkPi-assembly-0.1.0-SNAPSHOT.jar` file on your development system.</span><span class="sxs-lookup"><span data-stu-id="964ea-179">Update the jar path to the location of the `SparkPi-assembly-0.1.0-SNAPSHOT.jar` file on your development system.</span></span> <span data-ttu-id="964ea-180">You can also use your own custom jar file.</span><span class="sxs-lookup"><span data-stu-id="964ea-180">You can also use your own custom jar file.</span></span>

```bash
WORKDIR /opt/spark/work-dir

ADD /path/to/SparkPi-assembly-0.1.0-SNAPSHOT.jar SparkPi-assembly-0.1.0-SNAPSHOT.jar

ENTRYPOINT [ "/opt/entrypoint.sh" ]
```

<span data-ttu-id="964ea-181">Build and push the image with the included Spark scripts.</span><span class="sxs-lookup"><span data-stu-id="964ea-181">Build and push the image with the included Spark scripts.</span></span>

```bash
./bin/docker-image-tool.sh -r <your container repository name> -t <tag> build
./bin/docker-image-tool.sh -r <your container repository name> -t <tag> push
```

<span data-ttu-id="964ea-182">When running the job, instead of indicating a remote jar URL, the `local://` scheme can be used with the path to the jar file in the Docker image.</span><span class="sxs-lookup"><span data-stu-id="964ea-182">When running the job, instead of indicating a remote jar URL, the `local://` scheme can be used with the path to the jar file in the Docker image.</span></span>

```bash
./bin/spark-submit \
    --master k8s://https://<k8s-apiserver-host>:<k8s-apiserver-port> \
    --deploy-mode cluster \
    --name spark-pi \
    --class org.apache.spark.examples.SparkPi \
    --conf spark.executor.instances=3 \
    --conf spark.kubernetes.container.image=<spark-image> \
    local:///opt/spark/work-dir/<your-jar-name>.jar
```

> [!WARNING]
> <span data-ttu-id="964ea-183">From Spark [documentation][spark-docs]: "The Kubernetes scheduler is currently experimental.</span><span class="sxs-lookup"><span data-stu-id="964ea-183">From Spark [documentation][spark-docs]: "The Kubernetes scheduler is currently experimental.</span></span> <span data-ttu-id="964ea-184">In future versions, there may be behavioral changes around configuration, container images and entrypoints".</span><span class="sxs-lookup"><span data-stu-id="964ea-184">In future versions, there may be behavioral changes around configuration, container images and entrypoints".</span></span>

## <a name="next-steps"></a><span data-ttu-id="964ea-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="964ea-185">Next steps</span></span>

<span data-ttu-id="964ea-186">Check out Spark documentation for more details.</span><span class="sxs-lookup"><span data-stu-id="964ea-186">Check out Spark documentation for more details.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="964ea-187">[Spark documentation][spark-docs]</span><span class="sxs-lookup"><span data-stu-id="964ea-187">[Spark documentation][spark-docs]</span></span>

<!-- LINKS - external -->
[apache-spark]: https://spark.apache.org/
[docker-hub]: https://docs.docker.com/docker-hub/
[java-install]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[sbt-install]: https://www.scala-sbt.org/1.0/docs/Setup.html
[spark-docs]: https://spark.apache.org/docs/latest/running-on-kubernetes.html
[spark-latest-release]: https://spark.apache.org/releases/spark-release-2-3-0.html
[spark-quickstart]: https://spark.apache.org/docs/latest/quick-start.html


<!-- LINKS - internal -->
[acr-aks]: https://docs.microsoft.com/azure/container-registry/container-registry-auth-aks
[acr-create]: https://docs.microsoft.com/azure/container-registry/container-registry-get-started-azure-cli
[aks-quickstart]: https://docs.microsoft.com/azure/aks/
[azure-cli]: https://docs.microsoft.com/cli/azure/?view=azure-cli-latest
[storage-account]: https://docs.microsoft.com/azure/storage/common/storage-azure-cli
