---
title: Change and redeploy a microservice | Microsoft Docs
description: This tutorial shows you how to change and redeploy a microservice in Remote Monitoring
author: dominicbetts
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 04/19/2018
ms.topic: conceptual
ms.openlocfilehash: b337862ec2011ba9d78fe466bc8715f706e565cf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868897"
---
# <a name="customize-and-redeploy-a-microservice"></a><span data-ttu-id="44d2a-103">Customize and redeploy a microservice</span><span class="sxs-lookup"><span data-stu-id="44d2a-103">Customize and redeploy a microservice</span></span>

<span data-ttu-id="44d2a-104">This tutorial shows you how to edit one of the microservices in the Remote Monitoring solution, build an image of your microservice, deploy the image to your docker hub, and then use it in Remote Monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="44d2a-104">This tutorial shows you how to edit one of the microservices in the Remote Monitoring solution, build an image of your microservice, deploy the image to your docker hub, and then use it in Remote Monitoring solution.</span></span> <span data-ttu-id="44d2a-105">To introduce this concept, the tutorial uses a basic scenario where you call a microservice API and change the status message from "Alive and Well" to "New Edits Made Here!"</span><span class="sxs-lookup"><span data-stu-id="44d2a-105">To introduce this concept, the tutorial uses a basic scenario where you call a microservice API and change the status message from "Alive and Well" to "New Edits Made Here!"</span></span>

<span data-ttu-id="44d2a-106">Remote Monitoring solution uses microservices that are built using docker images  that are pulled from a docker hub.</span><span class="sxs-lookup"><span data-stu-id="44d2a-106">Remote Monitoring solution uses microservices that are built using docker images  that are pulled from a docker hub.</span></span> 

<span data-ttu-id="44d2a-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="44d2a-107">In this tutorial, you learn how to:</span></span>

>[!div class="checklist"]
> * <span data-ttu-id="44d2a-108">Edit and build a microservice in the Remote Monitoring solution</span><span class="sxs-lookup"><span data-stu-id="44d2a-108">Edit and build a microservice in the Remote Monitoring solution</span></span>
> * <span data-ttu-id="44d2a-109">Build a docker image</span><span class="sxs-lookup"><span data-stu-id="44d2a-109">Build a docker image</span></span>
> * <span data-ttu-id="44d2a-110">Push a docker image to your docker hub</span><span class="sxs-lookup"><span data-stu-id="44d2a-110">Push a docker image to your docker hub</span></span>
> * <span data-ttu-id="44d2a-111">Pull the new docker image</span><span class="sxs-lookup"><span data-stu-id="44d2a-111">Pull the new docker image</span></span>
> * <span data-ttu-id="44d2a-112">Visualize the changes</span><span class="sxs-lookup"><span data-stu-id="44d2a-112">Visualize the changes</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="44d2a-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="44d2a-113">Prerequisites</span></span>

<span data-ttu-id="44d2a-114">To follow this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="44d2a-114">To follow this tutorial, you need:</span></span>

>[!div class="checklist"]
> * [<span data-ttu-id="44d2a-115">Deploy the Remote Monitoring solution accelerator locally</span><span class="sxs-lookup"><span data-stu-id="44d2a-115">Deploy the Remote Monitoring solution accelerator locally</span></span>](iot-accelerators-remote-monitoring-deploy-local.md)
> * [<span data-ttu-id="44d2a-116">A Docker account</span><span class="sxs-lookup"><span data-stu-id="44d2a-116">A Docker account</span></span>](https://hub.docker.com/)
> * <span data-ttu-id="44d2a-117">[Postman](https://www.getpostman.com/) - Needed to view the API response</span><span class="sxs-lookup"><span data-stu-id="44d2a-117">[Postman](https://www.getpostman.com/) - Needed to view the API response</span></span>

## <a name="call-the-api-and-view-response-status"></a><span data-ttu-id="44d2a-118">Call the API and view response status</span><span class="sxs-lookup"><span data-stu-id="44d2a-118">Call the API and view response status</span></span>

<span data-ttu-id="44d2a-119">In this part, you call the default IoT hub manager microservice API.</span><span class="sxs-lookup"><span data-stu-id="44d2a-119">In this part, you call the default IoT hub manager microservice API.</span></span> <span data-ttu-id="44d2a-120">The API returns a status message that you change later on by customizing the microservice.</span><span class="sxs-lookup"><span data-stu-id="44d2a-120">The API returns a status message that you change later on by customizing the microservice.</span></span>

1. <span data-ttu-id="44d2a-121">Make sure the Remote Monitoring solution is running locally on your machine.</span><span class="sxs-lookup"><span data-stu-id="44d2a-121">Make sure the Remote Monitoring solution is running locally on your machine.</span></span>
2. <span data-ttu-id="44d2a-122">Locate where you downloaded Postman and open it.</span><span class="sxs-lookup"><span data-stu-id="44d2a-122">Locate where you downloaded Postman and open it.</span></span>
3. <span data-ttu-id="44d2a-123">In Postman, enter the following in the GET: http://localhost:8080/iothubmanager/v1/status.</span><span class="sxs-lookup"><span data-stu-id="44d2a-123">In Postman, enter the following in the GET: http://localhost:8080/iothubmanager/v1/status.</span></span>
4. <span data-ttu-id="44d2a-124">View the return and you should see, "Status": "OK:Alive and Well".</span><span class="sxs-lookup"><span data-stu-id="44d2a-124">View the return and you should see, "Status": "OK:Alive and Well".</span></span>
<span data-ttu-id="44d2a-125">![Alive and Well Postman Message](./media/iot-accelerators-microservices-example/postman-alive-well.png)</span><span class="sxs-lookup"><span data-stu-id="44d2a-125">![Alive and Well Postman Message](./media/iot-accelerators-microservices-example/postman-alive-well.png)</span></span>

## <a name="change-the-status-and-build-the-image"></a><span data-ttu-id="44d2a-126">Change the status and build the image</span><span class="sxs-lookup"><span data-stu-id="44d2a-126">Change the status and build the image</span></span>

<span data-ttu-id="44d2a-127">Now change the status message of the Iot Hub Manager microservice to "New Edits Made Here!"</span><span class="sxs-lookup"><span data-stu-id="44d2a-127">Now change the status message of the Iot Hub Manager microservice to "New Edits Made Here!"</span></span> <span data-ttu-id="44d2a-128">and then rebuild the docker image with this new status.</span><span class="sxs-lookup"><span data-stu-id="44d2a-128">and then rebuild the docker image with this new status.</span></span> <span data-ttu-id="44d2a-129">If you run into issues here, refer to our [Troubleshooting](#Troubleshoot) section.</span><span class="sxs-lookup"><span data-stu-id="44d2a-129">If you run into issues here, refer to our [Troubleshooting](#Troubleshoot) section.</span></span>

1. <span data-ttu-id="44d2a-130">Make sure your terminal is open and change to the directory where you have cloned the Remote Monitoring solution.</span><span class="sxs-lookup"><span data-stu-id="44d2a-130">Make sure your terminal is open and change to the directory where you have cloned the Remote Monitoring solution.</span></span> 
2. <span data-ttu-id="44d2a-131">Change your directory to "..azure-iot-pcs-remote-monitoring-dotnet/iothub-manager/WebService/v1/Controllers".</span><span class="sxs-lookup"><span data-stu-id="44d2a-131">Change your directory to "..azure-iot-pcs-remote-monitoring-dotnet/iothub-manager/WebService/v1/Controllers".</span></span>
3. <span data-ttu-id="44d2a-132">Open StatusController.cs in any text editor or IDE that you like.</span><span class="sxs-lookup"><span data-stu-id="44d2a-132">Open StatusController.cs in any text editor or IDE that you like.</span></span> 
4. <span data-ttu-id="44d2a-133">Locate the following code:</span><span class="sxs-lookup"><span data-stu-id="44d2a-133">Locate the following code:</span></span>

    ```javascript
    return new StatusApiModel(true, "Alive and well");
    ```

    <span data-ttu-id="44d2a-134">and change it to the code below and save it.</span><span class="sxs-lookup"><span data-stu-id="44d2a-134">and change it to the code below and save it.</span></span>

    ```javascript
    return new StatusApiModel(true, "New Edits Made Here!");
    ```

5. <span data-ttu-id="44d2a-135">Go back to your terminal but now change to the following directory: "...azure-iot-pcs-remote-monitoring-dotnet/iothub-manager/scripts/docker".</span><span class="sxs-lookup"><span data-stu-id="44d2a-135">Go back to your terminal but now change to the following directory: "...azure-iot-pcs-remote-monitoring-dotnet/iothub-manager/scripts/docker".</span></span>
6. <span data-ttu-id="44d2a-136">To build your new docker image, type</span><span class="sxs-lookup"><span data-stu-id="44d2a-136">To build your new docker image, type</span></span>

    ```cmd/sh
    sh build
    ```

7. <span data-ttu-id="44d2a-137">To verify your new image was successfully created, type</span><span class="sxs-lookup"><span data-stu-id="44d2a-137">To verify your new image was successfully created, type</span></span>

    ```cmd/sh
    docker images 
    ```

<span data-ttu-id="44d2a-138">The repository should be "azureiotpcs/iothub-manager-dotnet".</span><span class="sxs-lookup"><span data-stu-id="44d2a-138">The repository should be "azureiotpcs/iothub-manager-dotnet".</span></span>

![Successful docker image](./media/iot-accelerators-microservices-example/successful-docker-image.png)

## <a name="tag-and-push-the-image"></a><span data-ttu-id="44d2a-140">Tag and push the image</span><span class="sxs-lookup"><span data-stu-id="44d2a-140">Tag and push the image</span></span>
<span data-ttu-id="44d2a-141">Before you can push your new docker image to a docker hub, Docker expects your images to be tagged.</span><span class="sxs-lookup"><span data-stu-id="44d2a-141">Before you can push your new docker image to a docker hub, Docker expects your images to be tagged.</span></span> <span data-ttu-id="44d2a-142">If you run into issues here, refer to our [Troubleshooting](#Troubleshoot) section.</span><span class="sxs-lookup"><span data-stu-id="44d2a-142">If you run into issues here, refer to our [Troubleshooting](#Troubleshoot) section.</span></span>

1. <span data-ttu-id="44d2a-143">Locate the Image ID of the docker image you created by typing:</span><span class="sxs-lookup"><span data-stu-id="44d2a-143">Locate the Image ID of the docker image you created by typing:</span></span>

    ```cmd/sh
    docker images
    ```

2. <span data-ttu-id="44d2a-144">To tag your image with "testing" type</span><span class="sxs-lookup"><span data-stu-id="44d2a-144">To tag your image with "testing" type</span></span>

    ```cmd/sh
    docker tag [Image ID] [docker ID]/iothub-manager-dotnet:testing 
    ```

3. <span data-ttu-id="44d2a-145">To push your newly tagged image to your docker hub, type</span><span class="sxs-lookup"><span data-stu-id="44d2a-145">To push your newly tagged image to your docker hub, type</span></span>

    ```cmd/sh
    docker push [docker ID]/iothub-manager-dotnet:testing
    ```

4. <span data-ttu-id="44d2a-146">Open your internet browser and go to your [docker hub](https://hub.docker.com/) and sign in.</span><span class="sxs-lookup"><span data-stu-id="44d2a-146">Open your internet browser and go to your [docker hub](https://hub.docker.com/) and sign in.</span></span>
5. <span data-ttu-id="44d2a-147">You should now see your newly pushed docker image on your docker hub.</span><span class="sxs-lookup"><span data-stu-id="44d2a-147">You should now see your newly pushed docker image on your docker hub.</span></span>
<span data-ttu-id="44d2a-148">![Docker image in docker hub](./media/iot-accelerators-microservices-example/docker-image-in-docker-hub.png)</span><span class="sxs-lookup"><span data-stu-id="44d2a-148">![Docker image in docker hub](./media/iot-accelerators-microservices-example/docker-image-in-docker-hub.png)</span></span>

## <a name="update-your-remote-monitoring-solution"></a><span data-ttu-id="44d2a-149">Update your Remote Monitoring solution</span><span class="sxs-lookup"><span data-stu-id="44d2a-149">Update your Remote Monitoring solution</span></span>
<span data-ttu-id="44d2a-150">You now need to update your local docker-compose.yml to pull your new docker image from your docker hub.</span><span class="sxs-lookup"><span data-stu-id="44d2a-150">You now need to update your local docker-compose.yml to pull your new docker image from your docker hub.</span></span> <span data-ttu-id="44d2a-151">If you run into issues here, refer to our [Troubleshooting](#Troubleshoot) section.</span><span class="sxs-lookup"><span data-stu-id="44d2a-151">If you run into issues here, refer to our [Troubleshooting](#Troubleshoot) section.</span></span>

1. <span data-ttu-id="44d2a-152">Go back to the terminal and change to the following directory: "..azure-iot-pcs-remote-monitoring-dotnet/scripts/local".</span><span class="sxs-lookup"><span data-stu-id="44d2a-152">Go back to the terminal and change to the following directory: "..azure-iot-pcs-remote-monitoring-dotnet/scripts/local".</span></span>
2. <span data-ttu-id="44d2a-153">Open docker-compose.yml in any text editor or IDE that you like.</span><span class="sxs-lookup"><span data-stu-id="44d2a-153">Open docker-compose.yml in any text editor or IDE that you like.</span></span>
3. <span data-ttu-id="44d2a-154">Locate the following code:</span><span class="sxs-lookup"><span data-stu-id="44d2a-154">Locate the following code:</span></span>

    ```docker
    image: azureiotpcs/pcs-auth-dotnet:testing
    ```

    <span data-ttu-id="44d2a-155">and change it to look like the image below and save it.</span><span class="sxs-lookup"><span data-stu-id="44d2a-155">and change it to look like the image below and save it.</span></span>

    ```cmd/sh
    image: [docker ID]/pcs-auth-dotnet:testing
    ```

## <a name="view-the-new-response-status"></a><span data-ttu-id="44d2a-156">View the new response status</span><span class="sxs-lookup"><span data-stu-id="44d2a-156">View the new response status</span></span>
<span data-ttu-id="44d2a-157">Finish up by redeploying a local instance of the Remote Monitoring solution and viewing the new status response in Postman.</span><span class="sxs-lookup"><span data-stu-id="44d2a-157">Finish up by redeploying a local instance of the Remote Monitoring solution and viewing the new status response in Postman.</span></span>

1. <span data-ttu-id="44d2a-158">Go back to your terminal and change to the following directory: "..azure-iot-pcs-remote-monitoring-dotnet/scripts/local".</span><span class="sxs-lookup"><span data-stu-id="44d2a-158">Go back to your terminal and change to the following directory: "..azure-iot-pcs-remote-monitoring-dotnet/scripts/local".</span></span>
2. <span data-ttu-id="44d2a-159">Start your local instance of the Remote Monitoring solution by typing the following command into the terminal:</span><span class="sxs-lookup"><span data-stu-id="44d2a-159">Start your local instance of the Remote Monitoring solution by typing the following command into the terminal:</span></span>

    ```cmd/sh
    docker-compose up
    ```

3. <span data-ttu-id="44d2a-160">Locate where you downloaded Postman and open it.</span><span class="sxs-lookup"><span data-stu-id="44d2a-160">Locate where you downloaded Postman and open it.</span></span>
4. <span data-ttu-id="44d2a-161">In Postman, enter the following request in the GET: http://localhost:8080/iothubmanager/v1/status.</span><span class="sxs-lookup"><span data-stu-id="44d2a-161">In Postman, enter the following request in the GET: http://localhost:8080/iothubmanager/v1/status.</span></span> <span data-ttu-id="44d2a-162">You should now see, "Status": "OK: New Edits Made Here!".</span><span class="sxs-lookup"><span data-stu-id="44d2a-162">You should now see, "Status": "OK: New Edits Made Here!".</span></span>

![New Edits Made Here postman message](./media/iot-accelerators-microservices-example/new-postman-message.png)

## <a name="Troubleshoot"></a><span data-ttu-id="44d2a-164">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="44d2a-164">Troubleshoot</span></span>

<span data-ttu-id="44d2a-165">If you're running into issues, try removing the docker images and containers on the local machine.</span><span class="sxs-lookup"><span data-stu-id="44d2a-165">If you're running into issues, try removing the docker images and containers on the local machine.</span></span>

1. <span data-ttu-id="44d2a-166">To remove all containers, you'll first need to stop all running containers.</span><span class="sxs-lookup"><span data-stu-id="44d2a-166">To remove all containers, you'll first need to stop all running containers.</span></span> <span data-ttu-id="44d2a-167">Open your terminal and type</span><span class="sxs-lookup"><span data-stu-id="44d2a-167">Open your terminal and type</span></span>

    ```cmd/sh
    docker stop $(docker ps -aq)
    docker rm $(docker ps -aq)
    ```
    
2. <span data-ttu-id="44d2a-168">To remove all images, open your terminal and type</span><span class="sxs-lookup"><span data-stu-id="44d2a-168">To remove all images, open your terminal and type</span></span> 

    ```cmd/sh
    docker rmi $(docker images -q)
    ```

3. <span data-ttu-id="44d2a-169">You can check if there are any containers on the machine by typing</span><span class="sxs-lookup"><span data-stu-id="44d2a-169">You can check if there are any containers on the machine by typing</span></span>

    ```cmd/sh
    docker ps -aq 
    ```

    <span data-ttu-id="44d2a-170">If you successfully removed all containers, nothing should show up.</span><span class="sxs-lookup"><span data-stu-id="44d2a-170">If you successfully removed all containers, nothing should show up.</span></span>

4. <span data-ttu-id="44d2a-171">You can check if there are any images on the machine by typing</span><span class="sxs-lookup"><span data-stu-id="44d2a-171">You can check if there are any images on the machine by typing</span></span>

    ```cmd/sh
    docker images
    ```

    <span data-ttu-id="44d2a-172">If you successfully removed all containers, nothing should show up.</span><span class="sxs-lookup"><span data-stu-id="44d2a-172">If you successfully removed all containers, nothing should show up.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44d2a-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="44d2a-173">Next steps</span></span>

<span data-ttu-id="44d2a-174">In this tutorial, you saw how to:</span><span class="sxs-lookup"><span data-stu-id="44d2a-174">In this tutorial, you saw how to:</span></span>

<!-- Repeat task list from intro -->
>[!div class="checklist"]
> * <span data-ttu-id="44d2a-175">Edit and build a microservice in the Remote Monitoring solution</span><span class="sxs-lookup"><span data-stu-id="44d2a-175">Edit and build a microservice in the Remote Monitoring solution</span></span>
> * <span data-ttu-id="44d2a-176">Build a docker image</span><span class="sxs-lookup"><span data-stu-id="44d2a-176">Build a docker image</span></span>
> * <span data-ttu-id="44d2a-177">Push a docker image to your docker hub</span><span class="sxs-lookup"><span data-stu-id="44d2a-177">Push a docker image to your docker hub</span></span>
> * <span data-ttu-id="44d2a-178">Pull the new docker image</span><span class="sxs-lookup"><span data-stu-id="44d2a-178">Pull the new docker image</span></span>
> * <span data-ttu-id="44d2a-179">Visualize the changes</span><span class="sxs-lookup"><span data-stu-id="44d2a-179">Visualize the changes</span></span> 

<span data-ttu-id="44d2a-180">The next thing to try is [customizing the device simulator microservice in the Remote Monitoring solution](iot-accelerators-microservices-example.md)</span><span class="sxs-lookup"><span data-stu-id="44d2a-180">The next thing to try is [customizing the device simulator microservice in the Remote Monitoring solution](iot-accelerators-microservices-example.md)</span></span>

<span data-ttu-id="44d2a-181">For more developer information about the Remote Monitoring solution, see:</span><span class="sxs-lookup"><span data-stu-id="44d2a-181">For more developer information about the Remote Monitoring solution, see:</span></span>

* <span data-ttu-id="44d2a-182">[Developer Reference Guide](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Developer-Reference-Guide)
<!-- Next tutorials in the sequence --></span><span class="sxs-lookup"><span data-stu-id="44d2a-182">[Developer Reference Guide](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Developer-Reference-Guide)
<!-- Next tutorials in the sequence --></span></span>

