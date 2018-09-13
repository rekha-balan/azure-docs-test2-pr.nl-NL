---
title: Build a Python and PostgreSQL web app in Azure App Service | Microsoft Docs
description: Learn how to run a data-driven Python app in Azure, with connection to a PostgreSQL database.
services: app-service\web
documentationcenter: python
author: berndverst
manager: jeconnoc
ms.service: app-service-web
ms.workload: web
ms.devlang: python
ms.topic: tutorial
ms.date: 07/13/2018
ms.author: beverst;cephalin
ms.custom: mvc
ms.openlocfilehash: 9a623156ad2a27abf7fa5e865f8b7452e2c70b3c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864339"
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a><span data-ttu-id="5f5ee-103">Build a Docker Python and PostgreSQL web app in Azure</span><span class="sxs-lookup"><span data-stu-id="5f5ee-103">Build a Docker Python and PostgreSQL web app in Azure</span></span>

<span data-ttu-id="5f5ee-104">Web App for Containers provides a highly scalable, self-patching web hosting service.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-104">Web App for Containers provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="5f5ee-105">This tutorial shows how to create a data-driven Python web app, using PostgreSQL as the database back end.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-105">This tutorial shows how to create a data-driven Python web app, using PostgreSQL as the database back end.</span></span> <span data-ttu-id="5f5ee-106">When you are done, you have a Python Flask application running within a Docker container on [App Service on Linux](app-service-linux-intro.md).</span><span class="sxs-lookup"><span data-stu-id="5f5ee-106">When you are done, you have a Python Flask application running within a Docker container on [App Service on Linux](app-service-linux-intro.md).</span></span>

![Docker Python Flask app in App Service on Linux](./media/tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

<span data-ttu-id="5f5ee-108">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="5f5ee-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5f5ee-109">Create a PostgreSQL database in Azure</span><span class="sxs-lookup"><span data-stu-id="5f5ee-109">Create a PostgreSQL database in Azure</span></span>
> * <span data-ttu-id="5f5ee-110">Connect a Python app to PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="5f5ee-110">Connect a Python app to PostgreSQL</span></span>
> * <span data-ttu-id="5f5ee-111">Deploy the app to Azure</span><span class="sxs-lookup"><span data-stu-id="5f5ee-111">Deploy the app to Azure</span></span>
> * <span data-ttu-id="5f5ee-112">Update the data model and redeploy the app</span><span class="sxs-lookup"><span data-stu-id="5f5ee-112">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="5f5ee-113">Manage the app in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="5f5ee-113">Manage the app in the Azure portal</span></span>

<span data-ttu-id="5f5ee-114">You can follow the steps in this article on macOS.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-114">You can follow the steps in this article on macOS.</span></span> <span data-ttu-id="5f5ee-115">Linux and Windows instructions are the same in most cases, but the differences are not detailed in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-115">Linux and Windows instructions are the same in most cases, but the differences are not detailed in this tutorial.</span></span>
 
[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="5f5ee-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5f5ee-116">Prerequisites</span></span>

<span data-ttu-id="5f5ee-117">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="5f5ee-117">To complete this tutorial:</span></span>

1. [<span data-ttu-id="5f5ee-118">Install Git</span><span class="sxs-lookup"><span data-stu-id="5f5ee-118">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="5f5ee-119">Install Python</span><span class="sxs-lookup"><span data-stu-id="5f5ee-119">Install Python</span></span>](https://www.python.org/downloads/)
1. [<span data-ttu-id="5f5ee-120">Install and run PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="5f5ee-120">Install and run PostgreSQL</span></span>](https://www.postgresql.org/download/)
1. [<span data-ttu-id="5f5ee-121">Install Docker Community Edition</span><span class="sxs-lookup"><span data-stu-id="5f5ee-121">Install Docker Community Edition</span></span>](https://www.docker.com/community-edition)

## <a name="test-local-postgresql-installation-and-create-a-database"></a><span data-ttu-id="5f5ee-122">Test local PostgreSQL installation and create a database</span><span class="sxs-lookup"><span data-stu-id="5f5ee-122">Test local PostgreSQL installation and create a database</span></span>

<span data-ttu-id="5f5ee-123">In a local terminal window, run `psql` to connect to your local PostgreSQL server.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-123">In a local terminal window, run `psql` to connect to your local PostgreSQL server.</span></span>

```bash
sudo -u postgres psql
```

<span data-ttu-id="5f5ee-124">If your connection is successful, your PostgreSQL database is running.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-124">If your connection is successful, your PostgreSQL database is running.</span></span> <span data-ttu-id="5f5ee-125">If not, make sure that your local PostgresQL database is started by following the steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span><span class="sxs-lookup"><span data-stu-id="5f5ee-125">If not, make sure that your local PostgresQL database is started by following the steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="5f5ee-126">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-126">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span></span>

```sql
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration TO manager;
```

<span data-ttu-id="5f5ee-127">Type `\q` to exit the PostgreSQL client.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-127">Type `\q` to exit the PostgreSQL client.</span></span> 

<a name="step2"></a>

## <a name="create-local-python-app"></a><span data-ttu-id="5f5ee-128">Create local Python app</span><span class="sxs-lookup"><span data-stu-id="5f5ee-128">Create local Python app</span></span>

<span data-ttu-id="5f5ee-129">In this step, you set up the local Python Flask project.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-129">In this step, you set up the local Python Flask project.</span></span>

### <a name="clone-the-sample-app"></a><span data-ttu-id="5f5ee-130">Clone the sample app</span><span class="sxs-lookup"><span data-stu-id="5f5ee-130">Clone the sample app</span></span>

<span data-ttu-id="5f5ee-131">Open the terminal window, and `CD` to a working directory.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-131">Open the terminal window, and `CD` to a working directory.</span></span>

<span data-ttu-id="5f5ee-132">Run the following commands to clone the sample repository and go to the *0.1-initialapp* release.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-132">Run the following commands to clone the sample repository and go to the *0.1-initialapp* release.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

<span data-ttu-id="5f5ee-133">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-133">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span></span> 

### <a name="run-the-app-locally"></a><span data-ttu-id="5f5ee-134">Run the app locally</span><span class="sxs-lookup"><span data-stu-id="5f5ee-134">Run the app locally</span></span>

<span data-ttu-id="5f5ee-135">Install the required packages and start the application.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-135">Install the required packages and start the application.</span></span>

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="5f5ee-136">When the app is fully loaded, you see something similar to the following message:</span><span class="sxs-lookup"><span data-stu-id="5f5ee-136">When the app is fully loaded, you see something similar to the following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="5f5ee-137">Navigate to `http://localhost:5000` in a browser.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-137">Navigate to `http://localhost:5000` in a browser.</span></span> <span data-ttu-id="5f5ee-138">Click **Register!**</span><span class="sxs-lookup"><span data-stu-id="5f5ee-138">Click **Register!**</span></span> <span data-ttu-id="5f5ee-139">and create a test user.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-139">and create a test user.</span></span>

![Python Flask application running locally](./media/tutorial-docker-python-postgresql-app/local-app.png)

<span data-ttu-id="5f5ee-141">The Flask sample application stores user data in the database.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-141">The Flask sample application stores user data in the database.</span></span> <span data-ttu-id="5f5ee-142">If you are successful at registering a user, your app is writing data to the local PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-142">If you are successful at registering a user, your app is writing data to the local PostgreSQL database.</span></span>

<span data-ttu-id="5f5ee-143">To stop the Flask server at anytime, type Ctrl+C in the terminal.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-143">To stop the Flask server at anytime, type Ctrl+C in the terminal.</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-production-postgresql-database"></a><span data-ttu-id="5f5ee-144">Create a production PostgreSQL database</span><span class="sxs-lookup"><span data-stu-id="5f5ee-144">Create a production PostgreSQL database</span></span>

<span data-ttu-id="5f5ee-145">In this step, you create a PostgreSQL database in Azure.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-145">In this step, you create a PostgreSQL database in Azure.</span></span> <span data-ttu-id="5f5ee-146">When your app is deployed to Azure, it uses this cloud database.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-146">When your app is deployed to Azure, it uses this cloud database.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

### <a name="create-a-resource-group"></a><span data-ttu-id="5f5ee-147">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="5f5ee-147">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../../includes/app-service-web-create-resource-group-linux-no-h.md)] 

### <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="5f5ee-148">Create an Azure Database for PostgreSQL server</span><span class="sxs-lookup"><span data-stu-id="5f5ee-148">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="5f5ee-149">Create a PostgreSQL server with the [`az postgres server create`](/cli/azure/postgres/server?view=azure-cli-latest#az-postgres-server-create) command in the Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-149">Create a PostgreSQL server with the [`az postgres server create`](/cli/azure/postgres/server?view=azure-cli-latest#az-postgres-server-create) command in the Cloud Shell.</span></span>

<span data-ttu-id="5f5ee-150">In the following example command, replace *\<postgresql_name>* with a unique server name, and replace *\<admin_username>* and *\<admin_password>* with the desired user credentials.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-150">In the following example command, replace *\<postgresql_name>* with a unique server name, and replace *\<admin_username>* and *\<admin_password>* with the desired user credentials.</span></span> <span data-ttu-id="5f5ee-151">The server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so the name needs to be unique across all servers in Azure.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-151">The server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so the name needs to be unique across all servers in Azure.</span></span> <span data-ttu-id="5f5ee-152">The user credentials are for the database admin user account.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-152">The user credentials are for the database admin user account.</span></span> 

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --location "West Europe" --admin-user <admin_username> --admin-password <admin_password> --sku-name GP_Gen4_2
```

<span data-ttu-id="5f5ee-153">When the Azure Database for PostgreSQL server is created, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="5f5ee-153">When the Azure Database for PostgreSQL server is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "administratorLogin": "<admin_username>",
  "fullyQualifiedDomainName": "<postgresql_name>.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>",
  "location": "westus",
  "name": "<postgresql_name>",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": 100,
    "family": null,
    "name": "PGSQLS3M100",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

### <a name="create-a-firewall-rule-for-the-postgresql-server"></a><span data-ttu-id="5f5ee-154">Create a firewall rule for the PostgreSQL server</span><span class="sxs-lookup"><span data-stu-id="5f5ee-154">Create a firewall rule for the PostgreSQL server</span></span>

<span data-ttu-id="5f5ee-155">In the Cloud Shell, run the following Azure CLI command to allow access to the database from all IP addresses.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-155">In the Cloud Shell, run the following Azure CLI command to allow access to the database from all IP addresses.</span></span> 
> [!Note]
> <span data-ttu-id="5f5ee-156">It is not advised to leave all ports open to your database, or to make your database internet-facing.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-156">It is not advised to leave all ports open to your database, or to make your database internet-facing.</span></span>  <span data-ttu-id="5f5ee-157">See other [Azure security articles](https://docs.microsoft.com/azure/security/) to properly secure your new database for production use.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-157">See other [Azure security articles](https://docs.microsoft.com/azure/security/) to properly secure your new database for production use.</span></span>  

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=0.0.0.0 --name AllowAzureIPs
```

> [!TIP] 
> <span data-ttu-id="5f5ee-158">You can be even more restrictive in your firewall rule by [using only the outbound IP addresses your app uses](../app-service-ip-addresses.md?toc=%2fazure%2fapp-service%2fcontainers%2ftoc.json#find-outbound-ips).</span><span class="sxs-lookup"><span data-stu-id="5f5ee-158">You can be even more restrictive in your firewall rule by [using only the outbound IP addresses your app uses](../app-service-ip-addresses.md?toc=%2fazure%2fapp-service%2fcontainers%2ftoc.json#find-outbound-ips).</span></span>
>

<span data-ttu-id="5f5ee-159">In the Cloud Shell, run the command again to allow access to the database from your local computer by replacing *\<you_ip_address>* with [your local IPv4 IP address](https://whatismyipaddress.com/).</span><span class="sxs-lookup"><span data-stu-id="5f5ee-159">In the Cloud Shell, run the command again to allow access to the database from your local computer by replacing *\<you_ip_address>* with [your local IPv4 IP address](https://whatismyipaddress.com/).</span></span> 

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=<you_ip_address> --end-ip-address=<you_ip_address> --name AllowLocalClient
```

## <a name="connect-python-app-to-production-database"></a><span data-ttu-id="5f5ee-160">Connect Python app to production database</span><span class="sxs-lookup"><span data-stu-id="5f5ee-160">Connect Python app to production database</span></span>

<span data-ttu-id="5f5ee-161">In this step, you connect your Flask sample app to the Azure Database for PostgreSQL server you created.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-161">In this step, you connect your Flask sample app to the Azure Database for PostgreSQL server you created.</span></span>

### <a name="create-empty-database-and-user-access"></a><span data-ttu-id="5f5ee-162">Create empty database and user access</span><span class="sxs-lookup"><span data-stu-id="5f5ee-162">Create empty database and user access</span></span>

<span data-ttu-id="5f5ee-163">In the Cloud Shell, connect to the database by running `psql`.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-163">In the Cloud Shell, connect to the database by running `psql`.</span></span> <span data-ttu-id="5f5ee-164">When prompted for your admin password, use the same password you specified in [Create an Azure Database for PostgreSQL server](#create-an-azure-database-for-postgresql-server).</span><span class="sxs-lookup"><span data-stu-id="5f5ee-164">When prompted for your admin password, use the same password you specified in [Create an Azure Database for PostgreSQL server](#create-an-azure-database-for-postgresql-server).</span></span>

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

<span data-ttu-id="5f5ee-165">Create the database and user from the PostgreSQL CLI.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-165">Create the database and user from the PostgreSQL CLI.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration TO manager;
```

<span data-ttu-id="5f5ee-166">Type `\q` to exit the PostgreSQL client.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-166">Type `\q` to exit the PostgreSQL client.</span></span>

### <a name="test-app-connectivity-to-production-database"></a><span data-ttu-id="5f5ee-167">Test app connectivity to production database</span><span class="sxs-lookup"><span data-stu-id="5f5ee-167">Test app connectivity to production database</span></span>

<span data-ttu-id="5f5ee-168">Back in the local terminal window, run the following commands to run Flask database migration and the Flask server.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-168">Back in the local terminal window, run the following commands to run Flask database migration and the Flask server.</span></span>

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="5f5ee-169">When the app is fully loaded, you see something similar to the following message:</span><span class="sxs-lookup"><span data-stu-id="5f5ee-169">When the app is fully loaded, you see something similar to the following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="5f5ee-170">Navigate to http://localhost:5000 in a browser.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-170">Navigate to http://localhost:5000 in a browser.</span></span> <span data-ttu-id="5f5ee-171">Click **Register!**</span><span class="sxs-lookup"><span data-stu-id="5f5ee-171">Click **Register!**</span></span> <span data-ttu-id="5f5ee-172">and create a test registration.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-172">and create a test registration.</span></span> <span data-ttu-id="5f5ee-173">You are now writing data to the database in Azure.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-173">You are now writing data to the database in Azure.</span></span>

![Python Flask application running locally](./media/tutorial-docker-python-postgresql-app/local-app.png)

## <a name="upload-app-to-a-container-registry"></a><span data-ttu-id="5f5ee-175">Upload app to a container registry</span><span class="sxs-lookup"><span data-stu-id="5f5ee-175">Upload app to a container registry</span></span>

<span data-ttu-id="5f5ee-176">In this step, you create a Docker image and upload it to Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-176">In this step, you create a Docker image and upload it to Azure Container Registry.</span></span> <span data-ttu-id="5f5ee-177">You can also use popular registries like Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-177">You can also use popular registries like Docker Hub.</span></span>

### <a name="build-the-docker-image-and-test-it"></a><span data-ttu-id="5f5ee-178">Build the Docker image and test it</span><span class="sxs-lookup"><span data-stu-id="5f5ee-178">Build the Docker image and test it</span></span>

<span data-ttu-id="5f5ee-179">In the local terminal window, build the Docker image.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-179">In the local terminal window, build the Docker image.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
```

<span data-ttu-id="5f5ee-180">Docker displays a confirmation that it successfully created the image.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-180">Docker displays a confirmation that it successfully created the image.</span></span>

```bash
Successfully built 7548f983a36b
```

<span data-ttu-id="5f5ee-181">In the repository root, add an environment variable file called _db.env_, and then add the following database environment variables to it.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-181">In the repository root, add an environment variable file called _db.env_, and then add the following database environment variables to it.</span></span> <span data-ttu-id="5f5ee-182">The app connects to the Azure Database for PostgreSQL production database.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-182">The app connects to the Azure Database for PostgreSQL production database.</span></span>

```text
DBHOST=<postgresql_name>.postgres.database.azure.com
DBUSER=manager@<postgresql_name>
DBNAME=eventregistration
DBPASS=supersecretpass
```

<span data-ttu-id="5f5ee-183">Run the image locally in a Docker container.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-183">Run the image locally in a Docker container.</span></span> <span data-ttu-id="5f5ee-184">The following command specifies the environment variable file and maps the default Flask port 5000 to local port 5000.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-184">The following command specifies the environment variable file and maps the default Flask port 5000 to local port 5000.</span></span>

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

<span data-ttu-id="5f5ee-185">The output is similar to what you saw earlier.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-185">The output is similar to what you saw earlier.</span></span> <span data-ttu-id="5f5ee-186">However, the initial database migration no longer needs to be performed and therefore is skipped.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-186">However, the initial database migration no longer needs to be performed and therefore is skipped.</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="5f5ee-187">The database already contains the registration you created previously.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-187">The database already contains the registration you created previously.</span></span>

![Docker container-based Python Flask application running locally](./media/tutorial-docker-python-postgresql-app/local-docker.png)

<span data-ttu-id="5f5ee-189">Now that you verified that the container works locally, delete _db.env_.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-189">Now that you verified that the container works locally, delete _db.env_.</span></span> <span data-ttu-id="5f5ee-190">In Azure App Service, you will use app settings to define the environment variables.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-190">In Azure App Service, you will use app settings to define the environment variables.</span></span>  

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="5f5ee-191">Create an Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="5f5ee-191">Create an Azure Container Registry</span></span>

<span data-ttu-id="5f5ee-192">In the Cloud Shell, create a registry in Azure Container Registry with the following command.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-192">In the Cloud Shell, create a registry in Azure Container Registry with the following command.</span></span> <span data-ttu-id="5f5ee-193">Replace *\<registry_name>* with a unique registry name.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-193">Replace *\<registry_name>* with a unique registry name.</span></span>

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

### <a name="retrieve-registry-credentials"></a><span data-ttu-id="5f5ee-194">Retrieve registry credentials</span><span class="sxs-lookup"><span data-stu-id="5f5ee-194">Retrieve registry credentials</span></span>

<span data-ttu-id="5f5ee-195">In the Cloud Shell, run the following commands to retrieve the registry credentials.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-195">In the Cloud Shell, run the following commands to retrieve the registry credentials.</span></span> <span data-ttu-id="5f5ee-196">You need them to push and pull the images.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-196">You need them to push and pull the images.</span></span>

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

<span data-ttu-id="5f5ee-197">In the output, you see two passwords.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-197">In the output, you see two passwords.</span></span> <span data-ttu-id="5f5ee-198">Make note of the username (which is the registry name by default) and the first password.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-198">Make note of the username (which is the registry name by default) and the first password.</span></span>

```json
{
  "passwords": [
    {
      "name": "password",
      "value": "<registry_password>"
    },
    {
      "name": "password2",
      "value": "<registry_password2>"
    }
  ],
  "username": "<registry_name>"
}
```

### <a name="upload-docker-image-to-registry"></a><span data-ttu-id="5f5ee-199">Upload Docker image to registry</span><span class="sxs-lookup"><span data-stu-id="5f5ee-199">Upload Docker image to registry</span></span>

<span data-ttu-id="5f5ee-200">From the local terminal window, sign in to your new registry with `docker`.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-200">From the local terminal window, sign in to your new registry with `docker`.</span></span> <span data-ttu-id="5f5ee-201">When prompted, supply the password you retrieved.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-201">When prompted, supply the password you retrieved.</span></span>

```bash
docker login <registry_name>.azurecr.io -u <registry_name>
```

<span data-ttu-id="5f5ee-202">Push your Docker image to the registry.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-202">Push your Docker image to the registry.</span></span>

```bash
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="create-web-app-with-uploaded-image"></a><span data-ttu-id="5f5ee-203">Create web app with uploaded image</span><span class="sxs-lookup"><span data-stu-id="5f5ee-203">Create web app with uploaded image</span></span>

<span data-ttu-id="5f5ee-204">In this step, you create an app in Azure App Service and configure it to use the uploaded Docker image in Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-204">In this step, you create an app in Azure App Service and configure it to use the uploaded Docker image in Azure Container Registry.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="5f5ee-205">Create an App Service plan</span><span class="sxs-lookup"><span data-stu-id="5f5ee-205">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan](../../../includes/app-service-web-create-app-service-plan-linux-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="5f5ee-206">Create a web app</span><span class="sxs-lookup"><span data-stu-id="5f5ee-206">Create a web app</span></span>

<span data-ttu-id="5f5ee-207">In the Cloud Shell, create a web app in the *myAppServicePlan* App Service plan with the [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) command.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-207">In the Cloud Shell, create a web app in the *myAppServicePlan* App Service plan with the [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) command.</span></span>

<span data-ttu-id="5f5ee-208">In the following command, replace the *\<app_name>* placeholder with a unique app name.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-208">In the following command, replace the *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="5f5ee-209">This name is part of the default URL for the web app, so the name needs to be unique across all apps in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-209">This name is part of the default URL for the web app, so the name needs to be unique across all apps in Azure App Service.</span></span>

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan --deployment-container-image-name "<registry_name>.azurecr.io/flask-postgresql-sample"
```

<span data-ttu-id="5f5ee-210">When the web app has been created, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="5f5ee-210">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-environment-variables"></a><span data-ttu-id="5f5ee-211">Configure environment variables</span><span class="sxs-lookup"><span data-stu-id="5f5ee-211">Configure environment variables</span></span>

<span data-ttu-id="5f5ee-212">Earlier in the tutorial, you defined environment variables to connect to your PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-212">Earlier in the tutorial, you defined environment variables to connect to your PostgreSQL database.</span></span>

<span data-ttu-id="5f5ee-213">In App Service, you set environment variables as _app settings_ by using the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-213">In App Service, you set environment variables as _app settings_ by using the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command.</span></span>

<span data-ttu-id="5f5ee-214">The following example specifies the database connection details as app settings.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-214">The following example specifies the database connection details as app settings.</span></span> <span data-ttu-id="5f5ee-215">It also uses the *WEBSITES_PORT* variable to the container port 5000, which allows the container to receive HTTP traffic on port 80.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-215">It also uses the *WEBSITES_PORT* variable to the container port 5000, which allows the container to receive HTTP traffic on port 80.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" WEBSITES_PORT=5000
```

### <a name="configure-custom-container-deployment"></a><span data-ttu-id="5f5ee-216">Configure custom container deployment</span><span class="sxs-lookup"><span data-stu-id="5f5ee-216">Configure custom container deployment</span></span>

<span data-ttu-id="5f5ee-217">Even though you already specified the container image name, you still need to specify the custom registry URL and the user credentials.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-217">Even though you already specified the container image name, you still need to specify the custom registry URL and the user credentials.</span></span> <span data-ttu-id="5f5ee-218">In the Cloud Shell, run the [az webapp config container set](/cli/azure/webapp/config/container?view=azure-cli-latest#az-webapp-config-container-set) command.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-218">In the Cloud Shell, run the [az webapp config container set](/cli/azure/webapp/config/container?view=azure-cli-latest#az-webapp-config-container-set) command.</span></span>

```azurecli-interactive
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

<span data-ttu-id="5f5ee-219">In the Cloud Shell, restart the app.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-219">In the Cloud Shell, restart the app.</span></span> <span data-ttu-id="5f5ee-220">Restarting ensures that all settings are applied and the latest container is pulled from the registry.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-220">Restarting ensures that all settings are applied and the latest container is pulled from the registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="5f5ee-221">Browse to the Azure web app</span><span class="sxs-lookup"><span data-stu-id="5f5ee-221">Browse to the Azure web app</span></span> 

<span data-ttu-id="5f5ee-222">Browse to the deployed web app.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-222">Browse to the deployed web app.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
```

> [!NOTE]
> <span data-ttu-id="5f5ee-223">The web app takes some time to start because the container has to be downloaded and run when the app is requested the first time.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-223">The web app takes some time to start because the container has to be downloaded and run when the app is requested the first time.</span></span> <span data-ttu-id="5f5ee-224">If at first you see an error after a long time, just refresh the page.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-224">If at first you see an error after a long time, just refresh the page.</span></span>

<span data-ttu-id="5f5ee-225">You see previously registered guests that were saved to the Azure production database in the previous step.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-225">You see previously registered guests that were saved to the Azure production database in the previous step.</span></span>

![Docker container-based Python Flask application running locally](./media/tutorial-docker-python-postgresql-app/docker-app-deployed.png)

<span data-ttu-id="5f5ee-227">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="5f5ee-227">**Congratulations!**</span></span> <span data-ttu-id="5f5ee-228">You're running a Python app in Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-228">You're running a Python app in Web App for Containers.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="5f5ee-229">Update data model and redeploy</span><span class="sxs-lookup"><span data-stu-id="5f5ee-229">Update data model and redeploy</span></span>

<span data-ttu-id="5f5ee-230">In this step, you add the number of attendees to each event registration by updating the `Guest` model.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-230">In this step, you add the number of attendees to each event registration by updating the `Guest` model.</span></span>

<span data-ttu-id="5f5ee-231">In the local terminal window, check out the *0.2-migration* release with the following git command:</span><span class="sxs-lookup"><span data-stu-id="5f5ee-231">In the local terminal window, check out the *0.2-migration* release with the following git command:</span></span>

```bash
git checkout tags/0.2-migration
```

<span data-ttu-id="5f5ee-232">This release already made the necessary changes to the model, views, and controllers.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-232">This release already made the necessary changes to the model, views, and controllers.</span></span> <span data-ttu-id="5f5ee-233">It also includes a database migration generated via *alembic* (`flask db migrate`).</span><span class="sxs-lookup"><span data-stu-id="5f5ee-233">It also includes a database migration generated via *alembic* (`flask db migrate`).</span></span> <span data-ttu-id="5f5ee-234">You can see all changes made via the following git command:</span><span class="sxs-lookup"><span data-stu-id="5f5ee-234">You can see all changes made via the following git command:</span></span>

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="5f5ee-235">Test your changes locally</span><span class="sxs-lookup"><span data-stu-id="5f5ee-235">Test your changes locally</span></span>

<span data-ttu-id="5f5ee-236">In the local terminal window, run the following commands to test your changes locally by running the flask server.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-236">In the local terminal window, run the following commands to test your changes locally by running the flask server.</span></span>

```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="5f5ee-237">Navigate to http://localhost:5000 in your browser to view the changes.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-237">Navigate to http://localhost:5000 in your browser to view the changes.</span></span> <span data-ttu-id="5f5ee-238">Create a test registration.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-238">Create a test registration.</span></span>

![Docker container-based Python Flask application running locally](./media/tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-to-azure"></a><span data-ttu-id="5f5ee-240">Publish changes to Azure</span><span class="sxs-lookup"><span data-stu-id="5f5ee-240">Publish changes to Azure</span></span>

<span data-ttu-id="5f5ee-241">In the local terminal window, build the new docker image and push it to your registry.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-241">In the local terminal window, build the new docker image and push it to your registry.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

<span data-ttu-id="5f5ee-242">In the Cloud Shell, restart the app to make sure the latest container is pulled from the registry.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-242">In the Cloud Shell, restart the app to make sure the latest container is pulled from the registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

<span data-ttu-id="5f5ee-243">Navigate to your Azure web app and try out the new functionality again.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-243">Navigate to your Azure web app and try out the new functionality again.</span></span> <span data-ttu-id="5f5ee-244">Create another event registration.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-244">Create another event registration.</span></span>

```bash 
http://<app_name>.azurewebsites.net 
```

![Docker Python Flask app in Azure App Service](./media/tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="5f5ee-246">Manage your Azure web app</span><span class="sxs-lookup"><span data-stu-id="5f5ee-246">Manage your Azure web app</span></span>

<span data-ttu-id="5f5ee-247">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-247">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span>

<span data-ttu-id="5f5ee-248">From the left menu, click **App Services**, then click the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-248">From the left menu, click **App Services**, then click the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](./media/tutorial-docker-python-postgresql-app/app-resource.png)

<span data-ttu-id="5f5ee-250">By default, the portal shows your web app's **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-250">By default, the portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="5f5ee-251">This page gives you a view of how your app is doing.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-251">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="5f5ee-252">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-252">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="5f5ee-253">The tabs on the left side of the page show the different configuration pages you can open.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-253">The tabs on the left side of the page show the different configuration pages you can open.</span></span>

![App Service page in Azure portal](./media/tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a><span data-ttu-id="5f5ee-255">Next steps</span><span class="sxs-lookup"><span data-stu-id="5f5ee-255">Next steps</span></span>

<span data-ttu-id="5f5ee-256">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span><span class="sxs-lookup"><span data-stu-id="5f5ee-256">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5f5ee-257">Map an existing custom DNS name to Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="5f5ee-257">Map an existing custom DNS name to Azure Web Apps</span></span>](../app-service-web-tutorial-custom-domain.md)
