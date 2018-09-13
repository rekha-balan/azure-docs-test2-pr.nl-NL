---
title: Create a Python web app in Azure App Service on Linux | Microsoft Docs
description: Deploy your first Python hello world app in Azure App Service on Linux in minutes.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 09/07/2018
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: cc731723ee28b6edd13be73522c269ce209cd120
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966045"
---
# <a name="create-a-python-web-app-in-azure-app-service-on-linux-preview"></a><span data-ttu-id="a6c5d-103">Create a Python web app in Azure App Service on Linux (Preview)</span><span class="sxs-lookup"><span data-stu-id="a6c5d-103">Create a Python web app in Azure App Service on Linux (Preview)</span></span>

<span data-ttu-id="a6c5d-104">[App Service on Linux](app-service-linux-intro.md) provides a highly scalable, self-patching web hosting service using the Linux operating system.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-104">[App Service on Linux](app-service-linux-intro.md) provides a highly scalable, self-patching web hosting service using the Linux operating system.</span></span> <span data-ttu-id="a6c5d-105">This quickstart shows how to deploy a Python app on top of the built-in Python image (Preview) in App Service on Linux using the [Azure CLI](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a6c5d-105">This quickstart shows how to deploy a Python app on top of the built-in Python image (Preview) in App Service on Linux using the [Azure CLI](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="a6c5d-106">You can follow the steps in this article using a Mac, Windows, or Linux machine.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-106">You can follow the steps in this article using a Mac, Windows, or Linux machine.</span></span>

![Sample app running in Azure](media/quickstart-python/hello-world-in-browser.png)

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="a6c5d-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a6c5d-108">Prerequisites</span></span>

<span data-ttu-id="a6c5d-109">To complete this quickstart:</span><span class="sxs-lookup"><span data-stu-id="a6c5d-109">To complete this quickstart:</span></span>

* <span data-ttu-id="a6c5d-110"><a href="https://www.python.org/downloads/" target="_blank">Install Python 3.7</a></span><span class="sxs-lookup"><span data-stu-id="a6c5d-110"><a href="https://www.python.org/downloads/" target="_blank">Install Python 3.7</a></span></span>
* <span data-ttu-id="a6c5d-111"><a href="https://git-scm.com/" target="_blank">Install Git</a></span><span class="sxs-lookup"><span data-stu-id="a6c5d-111"><a href="https://git-scm.com/" target="_blank">Install Git</a></span></span>

## <a name="download-the-sample"></a><span data-ttu-id="a6c5d-112">Download the sample</span><span class="sxs-lookup"><span data-stu-id="a6c5d-112">Download the sample</span></span>

<span data-ttu-id="a6c5d-113">In a terminal window, run the following commands to clone the sample application to your local machine, and navigate to the directory with the sample code.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-113">In a terminal window, run the following commands to clone the sample application to your local machine, and navigate to the directory with the sample code.</span></span>

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
cd python-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="a6c5d-114">Run the app locally</span><span class="sxs-lookup"><span data-stu-id="a6c5d-114">Run the app locally</span></span>

<span data-ttu-id="a6c5d-115">Run the application locally so that you see how it should look when you deploy it to Azure.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-115">Run the application locally so that you see how it should look when you deploy it to Azure.</span></span> <span data-ttu-id="a6c5d-116">Open a terminal window and use the commands below to install the required dependencies and launch the built-in development server.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-116">Open a terminal window and use the commands below to install the required dependencies and launch the built-in development server.</span></span> 

```bash
# In Bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
FLASK_APP=application.py flask run

# In PowerShell
py -3 -m venv env
env\scripts\activate
pip install -r requirements.txt
set FLASK_APP=application.py
flask run
```

<span data-ttu-id="a6c5d-117">Open a web browser, and navigate to the sample app at `http://localhost:5000/`.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-117">Open a web browser, and navigate to the sample app at `http://localhost:5000/`.</span></span>

<span data-ttu-id="a6c5d-118">You see the **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="a6c5d-118">You see the **Hello World!**</span></span> <span data-ttu-id="a6c5d-119">message from the sample app displayed in the page.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-119">message from the sample app displayed in the page.</span></span>

![Sample app running locally](media/quickstart-python/hello-world-in-browser.png)

<span data-ttu-id="a6c5d-121">In your terminal window, press **Ctrl+C** to exit the web server.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-121">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../../includes/app-service-web-create-resource-group-linux.md)]

[!INCLUDE [Create app service plan](../../../includes/app-service-web-create-app-service-plan-linux.md)]

## <a name="create-a-web-app"></a><span data-ttu-id="a6c5d-122">Create a web app</span><span class="sxs-lookup"><span data-stu-id="a6c5d-122">Create a web app</span></span>

[!INCLUDE [Create app service plan](../../../includes/app-service-web-create-web-app-python-linux-no-h.md)]

<span data-ttu-id="a6c5d-123">Browse to the site to see your newly created web app with built-in image.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-123">Browse to the site to see your newly created web app with built-in image.</span></span> <span data-ttu-id="a6c5d-124">Replace _&lt;app name>_ with your web app name.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-124">Replace _&lt;app name>_ with your web app name.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="a6c5d-125">Here is what your new web app should look like:</span><span class="sxs-lookup"><span data-stu-id="a6c5d-125">Here is what your new web app should look like:</span></span>

![Empty web app page](media/quickstart-php/app-service-web-service-created.png)

[!INCLUDE [Push to Azure](../../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 42, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (39/39), done.
Writing objects: 100% (42/42), 9.43 KiB | 0 bytes/s, done.
Total 42 (delta 15), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'c40efbb40e'.
remote: Generating deployment script.
remote: Generating deployment script for python Web Site
.
.
.
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
remote: App container will begin restart within 10 seconds.
To https://user2234@cephalin-python.scm.azurewebsites.net/cephalin-python.git
 * [new branch]      master -> master
 ```

## <a name="browse-to-the-app"></a><span data-ttu-id="a6c5d-127">Browse to the app</span><span class="sxs-lookup"><span data-stu-id="a6c5d-127">Browse to the app</span></span>

<span data-ttu-id="a6c5d-128">Browse to the deployed application using your web browser.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-128">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="a6c5d-129">The Python sample code is running in a web app with built-in image.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-129">The Python sample code is running in a web app with built-in image.</span></span>

![Sample app running in Azure](media/quickstart-python/hello-world-in-browser.png)

<span data-ttu-id="a6c5d-131">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="a6c5d-131">**Congratulations!**</span></span> <span data-ttu-id="a6c5d-132">You've deployed your first Python app to App Service on Linux.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-132">You've deployed your first Python app to App Service on Linux.</span></span>

## <a name="update-locally-and-redeploy-the-code"></a><span data-ttu-id="a6c5d-133">Update locally and redeploy the code</span><span class="sxs-lookup"><span data-stu-id="a6c5d-133">Update locally and redeploy the code</span></span>

<span data-ttu-id="a6c5d-134">In the local repository, open the `application.py` file, and make a small change to the text in the last line:</span><span class="sxs-lookup"><span data-stu-id="a6c5d-134">In the local repository, open the `application.py` file, and make a small change to the text in the last line:</span></span>

```python
return "Hello Azure!"
```

<span data-ttu-id="a6c5d-135">Commit your changes in Git, and then push the code changes to Azure.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-135">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="a6c5d-136">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and refresh the page.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-136">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and refresh the page.</span></span>

![Updated sample app running in Azure](media/quickstart-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="a6c5d-138">Manage your new Azure web app</span><span class="sxs-lookup"><span data-stu-id="a6c5d-138">Manage your new Azure web app</span></span>

<span data-ttu-id="a6c5d-139">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-139">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="a6c5d-140">From the left menu, click **App Services**, and then click the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-140">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](./media/quickstart-python/app-service-list.png)

<span data-ttu-id="a6c5d-142">You see your web app's Overview page.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-142">You see your web app's Overview page.</span></span> <span data-ttu-id="a6c5d-143">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-143">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span>

![App Service page in Azure portal](media/quickstart-python/app-service-detail.png)

<span data-ttu-id="a6c5d-145">The left menu provides different pages for configuring your app.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-145">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="a6c5d-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="a6c5d-146">Next steps</span></span>

<span data-ttu-id="a6c5d-147">The built-in Python image in App Service on Linux is currently in Preview.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-147">The built-in Python image in App Service on Linux is currently in Preview.</span></span> <span data-ttu-id="a6c5d-148">You can create production Python apps using a custom container instead.</span><span class="sxs-lookup"><span data-stu-id="a6c5d-148">You can create production Python apps using a custom container instead.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a6c5d-149">Python with PostgreSQL in a custom container</span><span class="sxs-lookup"><span data-stu-id="a6c5d-149">Python with PostgreSQL in a custom container</span></span>](tutorial-docker-python-postgresql-app.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="a6c5d-150">Use custom images</span><span class="sxs-lookup"><span data-stu-id="a6c5d-150">Use custom images</span></span>](tutorial-custom-docker-image.md)