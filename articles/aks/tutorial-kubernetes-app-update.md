---
title: Kubernetes on Azure tutorial - Update an application
description: In this Azure Kubernetes Service (AKS) tutorial, you learn how to update an existing application deployment to AKS with a new version of the application code.
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: tutorial
ms.date: 08/14/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b2dd52fec112b879e072d3ac5598dd7978e68cbc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865201"
---
# <a name="tutorial-update-an-application-in-azure-kubernetes-service-aks"></a>Tutorial: Update an application in Azure Kubernetes Service (AKS)

After an application has been deployed in Kubernetes, it can be updated by specifying a new container image or image version. When doing so, the update is staged so that only a portion of the deployment is concurrently updated. This staged update enables the application to keep running during the update. It also provides a rollback mechanism if a deployment failure occurs.

In this tutorial, part six of seven, the sample Azure Vote app is updated. You learn how to:

> [!div class="checklist"]
> * Update the front-end application code
> * Create an updated container image
> * Push the container image to Azure Container Registry
> * Deploy the updated container image

## <a name="before-you-begin"></a>Before you begin

In previous tutorials, an application was packaged into a container image, the image uploaded to Azure Container Registry (ACR), and a Kubernetes cluster created. The application was then run on the Kubernetes cluster.

An application repository was also cloned that includes the application source code, and a pre-created Docker Compose file used in this tutorial. Verify that you have created a clone of the repo, and that you have changed directories into the cloned directory. If you haven't completed these steps, and want to follow along, return to [Tutorial 1 – Create container images][aks-tutorial-prepare-app].

This tutorial requires that you are running the Azure CLI version 2.0.44 or later. Run `az --version` to find the version. If you need to install or upgrade, see [Install Azure CLI][azure-cli-install].

## <a name="update-an-application"></a>Update an application

Let's make a change to the sample application, then update the version already deployed to your AKS cluster. The sample application source code can be found inside of the *azure-vote* directory. Open the *config_file.cfg* file with an editor, such as `vi`:

```console
vi azure-vote/azure-vote/config_file.cfg
```

Change the values for *VOTE1VALUE* and *VOTE2VALUE* to different colors. The following example shows the updated color values:

```
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

Save and close the file.

## <a name="update-the-container-image"></a>Update the container image

To re-create the front-end image and test the updated application, use [docker-compose][docker-compose]. The `--build` argument is used to instruct Docker Compose to re-create the application image:

```console
docker-compose up --build -d
```

## <a name="test-the-application-locally"></a>Test the application locally

To verify that the updated container image shows your changes, open a local web browser to http://localhost:8080.

![Image of Kubernetes cluster on Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

The updated color values provided in the *config_file.cfg* file are displayed on your running application.

## <a name="tag-and-push-the-image"></a>Tag and push the image

To correctly use the updated image, tag the *azure-vote-front* image with the login server name of your ACR registry. Get the login server name with the [az acr list](/cli/azure/acr#az_acr_list) command:

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Use [docker tag][docker-tag] to tag the image. Replace `<acrLoginServer>` with your ACR login server name or public registry hostname, and update the image version to *:v2* as follows:

```console
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:v2
```

Now use [docker push][docker-push] to upload the image to your registry. Replace `<acrLoginServer>` with your ACR login server name. If you experience issues pushing to your ACR registry, ensure that you have run the [az acr login][az-acr-login] command.

```console
docker push <acrLoginServer>/azure-vote-front:v2
```

## <a name="deploy-the-updated-application"></a>Deploy the updated application

To ensure maximum uptime, multiple instances of the application pod must be running. Verify the number of running front-end instances with the [kubectl get pods][kubectl-get] command:

```
$ kubectl get pods

NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

If you do not have multiple front-end pods, scale the *azure-vote-front* deployment as follows:

```console
kubectl scale --replicas=3 deployment/azure-vote-front
```

To update the application, use the [kubectl set][kubectl-set] command. Update `<acrLoginServer>` with the login server or host name of your container registry, and specify the *v2* application version:

```console
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:v2
```

To monitor the deployment, use the [kubectl get pod][kubectl-get] command. As the updated application is deployed, your pods are terminated and re-created with the new container image.

```console
kubectl get pods
```

The following example output shows pods terminating and new instances running as the deployment progresses:

```
$ kubectl get pods

NAME                               READY     STATUS        RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running       0          5m
azure-vote-front-1297194256-tpjlg  1/1       Running       0          1m
azure-vote-front-1297194256-tptnx  1/1       Running       0          5m
azure-vote-front-1297194256-zktw9  1/1       Terminating   0          1m
```

## <a name="test-the-updated-application"></a>Test the updated application

To view the update application, first get the external IP address of the `azure-vote-front` service:

```console
kubectl get service azure-vote-front
```

Now open a local web browser to the IP address.

![Image of Kubernetes cluster on Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a>Next steps

In this tutorial, you updated an application and rolled out this update to a Kubernetes cluster. You learned how to:

> [!div class="checklist"]
> * Update the front-end application code
> * Create an updated container image
> * Push the container image to Azure Container Registry
> * Deploy the updated container image

Advance to the next tutorial to learn how to upgrade an AKS cluster to a new version of Kubernetes.

> [!div class="nextstepaction"]
> [Upgrade Kubernetes][aks-tutorial-upgrade]

<!-- LINKS - external -->
[docker-compose]: https://docs.docker.com/compose/
[docker-push]: https://docs.docker.com/engine/reference/commandline/push/
[docker-tag]: https://docs.docker.com/engine/reference/commandline/tag/
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[kubectl-set]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#set

<!-- LINKS - internal -->
[aks-tutorial-prepare-app]: ./tutorial-kubernetes-prepare-app.md
[aks-tutorial-upgrade]: ./tutorial-kubernetes-upgrade-cluster.md
[az-acr-login]: /cli/azure/acr#az_acr_login
[azure-cli-install]: /cli/azure/install-azure-cli
