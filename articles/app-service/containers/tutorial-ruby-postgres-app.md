---
title: Build a Ruby and Postgres web app in Azure App Service on Linux | Microsoft Docs
description: Learn how to get a Ruby app working in Azure, with connection to a PostgreSQL database in Azure.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: cfowler
ms.service: app-service-web
ms.workload: web
ms.devlang: ruby
ms.topic: tutorial
ms.date: 06/15/2018
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 925537b3dff852921aad1e74d009e09fc90c394a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969074"
---
# <a name="build-a-ruby-and-postgres-web-app-in-azure-app-service-on-linux"></a><span data-ttu-id="f5c0e-103">Build a Ruby and Postgres web app in Azure App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="f5c0e-103">Build a Ruby and Postgres web app in Azure App Service on Linux</span></span>

<span data-ttu-id="f5c0e-104">[App Service on Linux](app-service-linux-intro.md) provides a highly scalable, self-patching web hosting service using the Linux operating system.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-104">[App Service on Linux](app-service-linux-intro.md) provides a highly scalable, self-patching web hosting service using the Linux operating system.</span></span> <span data-ttu-id="f5c0e-105">This tutorial shows how to create a Ruby web app and connect it to a PostgreSQL database.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-105">This tutorial shows how to create a Ruby web app and connect it to a PostgreSQL database.</span></span> <span data-ttu-id="f5c0e-106">When you're finished, you'll have a [Ruby on Rails](http://rubyonrails.org/) app running on App Service on Linux.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-106">When you're finished, you'll have a [Ruby on Rails](http://rubyonrails.org/) app running on App Service on Linux.</span></span>

![Ruby on Rails app running in Azure App Service](./media/tutorial-ruby-postgres-app/complete-checkbox-published.png)

<span data-ttu-id="f5c0e-108">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="f5c0e-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f5c0e-109">Create a PostgreSQL database in Azure</span><span class="sxs-lookup"><span data-stu-id="f5c0e-109">Create a PostgreSQL database in Azure</span></span>
> * <span data-ttu-id="f5c0e-110">Connect a Ruby on Rails app to PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="f5c0e-110">Connect a Ruby on Rails app to PostgreSQL</span></span>
> * <span data-ttu-id="f5c0e-111">Deploy the app to Azure</span><span class="sxs-lookup"><span data-stu-id="f5c0e-111">Deploy the app to Azure</span></span>
> * <span data-ttu-id="f5c0e-112">Update the data model and redeploy the app</span><span class="sxs-lookup"><span data-stu-id="f5c0e-112">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="f5c0e-113">Stream diagnostic logs from Azure</span><span class="sxs-lookup"><span data-stu-id="f5c0e-113">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="f5c0e-114">Manage the app in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f5c0e-114">Manage the app in the Azure portal</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="f5c0e-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f5c0e-115">Prerequisites</span></span>

<span data-ttu-id="f5c0e-116">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="f5c0e-116">To complete this tutorial:</span></span>

* [<span data-ttu-id="f5c0e-117">Install Git</span><span class="sxs-lookup"><span data-stu-id="f5c0e-117">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="f5c0e-118">Install Ruby 2.3</span><span class="sxs-lookup"><span data-stu-id="f5c0e-118">Install Ruby 2.3</span></span>](https://www.ruby-lang.org/en/documentation/installation/)
* [<span data-ttu-id="f5c0e-119">Install Ruby on Rails 5.1</span><span class="sxs-lookup"><span data-stu-id="f5c0e-119">Install Ruby on Rails 5.1</span></span>](http://guides.rubyonrails.org/v5.1/getting_started.html)
* [<span data-ttu-id="f5c0e-120">Install and run PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="f5c0e-120">Install and run PostgreSQL</span></span>](https://www.postgresql.org/download/)

## <a name="prepare-local-postgres"></a><span data-ttu-id="f5c0e-121">Prepare local Postgres</span><span class="sxs-lookup"><span data-stu-id="f5c0e-121">Prepare local Postgres</span></span>

<span data-ttu-id="f5c0e-122">In this step, you create a database in your local Postgres server for your use in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-122">In this step, you create a database in your local Postgres server for your use in this tutorial.</span></span>

### <a name="connect-to-local-postgres-server"></a><span data-ttu-id="f5c0e-123">Connect to local Postgres server</span><span class="sxs-lookup"><span data-stu-id="f5c0e-123">Connect to local Postgres server</span></span>

<span data-ttu-id="f5c0e-124">Open the terminal window and run `psql` to connect to your local Postgres server.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-124">Open the terminal window and run `psql` to connect to your local Postgres server.</span></span>

```bash
sudo -u postgres psql
```

<span data-ttu-id="f5c0e-125">If your connection is successful, your Postgres database is running.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-125">If your connection is successful, your Postgres database is running.</span></span> <span data-ttu-id="f5c0e-126">If not, make sure that your local Postgres database is started by following the steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span><span class="sxs-lookup"><span data-stu-id="f5c0e-126">If not, make sure that your local Postgres database is started by following the steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="f5c0e-127">Type `\q` to exit the Postgres client.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-127">Type `\q` to exit the Postgres client.</span></span> 

<span data-ttu-id="f5c0e-128">Create a Postgres user that can create databases by running the following command, using your signed-in Linux username.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-128">Create a Postgres user that can create databases by running the following command, using your signed-in Linux username.</span></span>

```bash
sudo -u postgres createuser -d <signed_in_user>
```

<a name="step2"></a>

## <a name="create-a-ruby-on-rails-app-locally"></a><span data-ttu-id="f5c0e-129">Create a Ruby on Rails app locally</span><span class="sxs-lookup"><span data-stu-id="f5c0e-129">Create a Ruby on Rails app locally</span></span>
<span data-ttu-id="f5c0e-130">In this step, you get a Ruby on Rails sample application, configure its database connection, and run it locally.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-130">In this step, you get a Ruby on Rails sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-the-sample"></a><span data-ttu-id="f5c0e-131">Clone the sample</span><span class="sxs-lookup"><span data-stu-id="f5c0e-131">Clone the sample</span></span>

<span data-ttu-id="f5c0e-132">In the terminal window, `cd` to a working directory.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-132">In the terminal window, `cd` to a working directory.</span></span>

<span data-ttu-id="f5c0e-133">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-133">Run the following command to clone the sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/rubyrails-tasks.git
```

<span data-ttu-id="f5c0e-134">`cd` to your cloned directory.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-134">`cd` to your cloned directory.</span></span> <span data-ttu-id="f5c0e-135">Install the required packages.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-135">Install the required packages.</span></span>

```bash
cd rubyrails-tasks
bundle install --path vendor/bundle
```

### <a name="run-the-sample-locally"></a><span data-ttu-id="f5c0e-136">Run the sample locally</span><span class="sxs-lookup"><span data-stu-id="f5c0e-136">Run the sample locally</span></span>

<span data-ttu-id="f5c0e-137">Run [the Rails migrations](http://guides.rubyonrails.org/active_record_migrations.html#running-migrations) to create the tables the application needs.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-137">Run [the Rails migrations](http://guides.rubyonrails.org/active_record_migrations.html#running-migrations) to create the tables the application needs.</span></span> <span data-ttu-id="f5c0e-138">To see which tables are created in the migrations, look in the _db/migrate_ directory in the Git repository.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-138">To see which tables are created in the migrations, look in the _db/migrate_ directory in the Git repository.</span></span>

```bash
rake db:create
rake db:migrate
```

<span data-ttu-id="f5c0e-139">Run the application.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-139">Run the application.</span></span>

```bash
rails server
```

<span data-ttu-id="f5c0e-140">Navigate to `http://localhost:3000` in a browser.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-140">Navigate to `http://localhost:3000` in a browser.</span></span> <span data-ttu-id="f5c0e-141">Add a few tasks in the page.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-141">Add a few tasks in the page.</span></span>

![Ruby on Rails connects successfully to Postgres](./media/tutorial-ruby-postgres-app/postgres-connect-success.png)

<span data-ttu-id="f5c0e-143">To stop the Rails server, type `Ctrl + C` in the terminal.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-143">To stop the Rails server, type `Ctrl + C` in the terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-postgres-in-azure"></a><span data-ttu-id="f5c0e-144">Create Postgres in Azure</span><span class="sxs-lookup"><span data-stu-id="f5c0e-144">Create Postgres in Azure</span></span>

<span data-ttu-id="f5c0e-145">In this step, you create a Postgres database in [Azure Database for PostgreSQL](/azure/postgresql/).</span><span class="sxs-lookup"><span data-stu-id="f5c0e-145">In this step, you create a Postgres database in [Azure Database for PostgreSQL](/azure/postgresql/).</span></span> <span data-ttu-id="f5c0e-146">Later, you configure the Ruby on Rails application to connect to this database.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-146">Later, you configure the Ruby on Rails application to connect to this database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="f5c0e-147">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="f5c0e-147">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../../includes/app-service-web-create-resource-group-linux-no-h.md)] 

### <a name="create-a-postgres-server"></a><span data-ttu-id="f5c0e-148">Create a Postgres server</span><span class="sxs-lookup"><span data-stu-id="f5c0e-148">Create a Postgres server</span></span>

<span data-ttu-id="f5c0e-149">Create a PostgreSQL server with the [`az postgres server create`](/cli/azure/postgres/server?view=azure-cli-latest#az-postgres-server-create) command.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-149">Create a PostgreSQL server with the [`az postgres server create`](/cli/azure/postgres/server?view=azure-cli-latest#az-postgres-server-create) command.</span></span>

<span data-ttu-id="f5c0e-150">Run the following command in the Cloud Shell, and substitute a unique server name for the *\<postgres_server_name>* placeholder.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-150">Run the following command in the Cloud Shell, and substitute a unique server name for the *\<postgres_server_name>* placeholder.</span></span> <span data-ttu-id="f5c0e-151">The server name needs to be unique across all servers in Azure.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-151">The server name needs to be unique across all servers in Azure.</span></span> 

```azurecli-interactive
az postgres server create --location "West Europe" --resource-group myResourceGroup --name <postgres_server_name> --admin-user adminuser --admin-password My5up3r$tr0ngPa$w0rd! --sku-name GP_Gen4_2
```

<span data-ttu-id="f5c0e-152">When the Azure Database for PostgreSQL server is created, the Azure CLI shows information similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="f5c0e-152">When the Azure Database for PostgreSQL server is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "administratorLogin": "adminuser",
  "earliestRestoreDate": "2018-06-15T12:38:25.280000+00:00",
  "fullyQualifiedDomainName": "<postgres_server_name>.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgres_server_name>",
  "location": "westeurope",
  "name": "<postgres_server_name>",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": 2,
    "family": "Gen4",
    "name": "GP_Gen4_2",
    "size": null,
    "tier": "GeneralPurpose"
  },
  < Output has been truncated for readability >
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="f5c0e-153">Configure server firewall</span><span class="sxs-lookup"><span data-stu-id="f5c0e-153">Configure server firewall</span></span>

<span data-ttu-id="f5c0e-154">In the Cloud Shell, create a firewall rule for your Postgres server to allow client connections by using the [`az postgres server firewall-rule create`](/cli/azure/postgres/server/firewall-rule?view=azure-cli-latest#az-postgres-server-firewall-rule-create) command.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-154">In the Cloud Shell, create a firewall rule for your Postgres server to allow client connections by using the [`az postgres server firewall-rule create`](/cli/azure/postgres/server/firewall-rule?view=azure-cli-latest#az-postgres-server-firewall-rule-create) command.</span></span> <span data-ttu-id="f5c0e-155">When both starting IP and end IP are set to 0.0.0.0, the firewall is only opened for other Azure resources.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-155">When both starting IP and end IP are set to 0.0.0.0, the firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="f5c0e-156">Substitute a unique server name for the *\<postgres_server_name>* placeholder.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-156">Substitute a unique server name for the *\<postgres_server_name>* placeholder.</span></span>

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server <postgres_server_name> --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!TIP] 
> <span data-ttu-id="f5c0e-157">You can be even more restrictive in your firewall rule by [using only the outbound IP addresses your app uses](../app-service-ip-addresses.md?toc=%2fazure%2fapp-service%2fcontainers%2ftoc.json#find-outbound-ips).</span><span class="sxs-lookup"><span data-stu-id="f5c0e-157">You can be even more restrictive in your firewall rule by [using only the outbound IP addresses your app uses](../app-service-ip-addresses.md?toc=%2fazure%2fapp-service%2fcontainers%2ftoc.json#find-outbound-ips).</span></span>
>

### <a name="connect-to-production-postgres-server-locally"></a><span data-ttu-id="f5c0e-158">Connect to production Postgres server locally</span><span class="sxs-lookup"><span data-stu-id="f5c0e-158">Connect to production Postgres server locally</span></span>

<span data-ttu-id="f5c0e-159">In the Cloud Shell, connect to the Postgres server in Azure.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-159">In the Cloud Shell, connect to the Postgres server in Azure.</span></span> <span data-ttu-id="f5c0e-160">Use the value you specified previously for the _&lt;postgres_server_name>_ placeholders.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-160">Use the value you specified previously for the _&lt;postgres_server_name>_ placeholders.</span></span>

```bash
psql -U adminuser@<postgres_server_name> -h <postgres_server_name>.postgres.database.azure.com postgres
```

<span data-ttu-id="f5c0e-161">When prompted for a password, use _My5up3r$tr0ngPa$w0rd!_, which you specified when you created the database server.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-161">When prompted for a password, use _My5up3r$tr0ngPa$w0rd!_, which you specified when you created the database server.</span></span>

### <a name="create-a-production-database"></a><span data-ttu-id="f5c0e-162">Create a production database</span><span class="sxs-lookup"><span data-stu-id="f5c0e-162">Create a production database</span></span>

<span data-ttu-id="f5c0e-163">At the `postgres` prompt, create a database.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-163">At the `postgres` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="f5c0e-164">Create a user with permissions</span><span class="sxs-lookup"><span data-stu-id="f5c0e-164">Create a user with permissions</span></span>

<span data-ttu-id="f5c0e-165">Create a database user called _railsappuser_ and give it all privileges in the `sampledb` database.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-165">Create a database user called _railsappuser_ and give it all privileges in the `sampledb` database.</span></span>

```sql
CREATE USER railsappuser WITH PASSWORD 'MyPostgresAzure2017'; 
GRANT ALL PRIVILEGES ON DATABASE sampledb TO railsappuser;
```

<span data-ttu-id="f5c0e-166">Exit the server connection by typing `\q`.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-166">Exit the server connection by typing `\q`.</span></span>

## <a name="connect-app-to-azure-postgres"></a><span data-ttu-id="f5c0e-167">Connect app to Azure Postgres</span><span class="sxs-lookup"><span data-stu-id="f5c0e-167">Connect app to Azure Postgres</span></span>

<span data-ttu-id="f5c0e-168">In this step, you connect the Ruby on Rails application to the Postgres database you created in Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-168">In this step, you connect the Ruby on Rails application to the Postgres database you created in Azure Database for PostgreSQL.</span></span>

<a name="devconfig"></a>

### <a name="configure-the-database-connection"></a><span data-ttu-id="f5c0e-169">Configure the database connection</span><span class="sxs-lookup"><span data-stu-id="f5c0e-169">Configure the database connection</span></span>

<span data-ttu-id="f5c0e-170">In the repository, open _config/database.yml_.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-170">In the repository, open _config/database.yml_.</span></span> <span data-ttu-id="f5c0e-171">At the bottom of the file, replace the production variables with the following code.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-171">At the bottom of the file, replace the production variables with the following code.</span></span> 

```txt
production:
  <<: *default
  host: <%= ENV['DB_HOST'] %>
  database: <%= ENV['DB_DATABASE'] %>
  username: <%= ENV['DB_USERNAME'] %>
  password: <%= ENV['DB_PASSWORD'] %>
```

<span data-ttu-id="f5c0e-172">Save the changes.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-172">Save the changes.</span></span>

### <a name="test-the-application-locally"></a><span data-ttu-id="f5c0e-173">Test the application locally</span><span class="sxs-lookup"><span data-stu-id="f5c0e-173">Test the application locally</span></span>

<span data-ttu-id="f5c0e-174">Back in the local terminal, set the following environment variables:</span><span class="sxs-lookup"><span data-stu-id="f5c0e-174">Back in the local terminal, set the following environment variables:</span></span>

```bash
export DB_HOST=<postgres_server_name>.postgres.database.azure.com
export DB_DATABASE=sampledb 
export DB_USERNAME=railsappuser@<postgres_server_name>
export DB_PASSWORD=MyPostgresAzure2017
```

<span data-ttu-id="f5c0e-175">Run Rails database migrations with the production values you just configured to create the tables in your Postgres database in Azure Database for PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-175">Run Rails database migrations with the production values you just configured to create the tables in your Postgres database in Azure Database for PostgreSQL.</span></span> 

```bash
rake db:migrate RAILS_ENV=production
```

<span data-ttu-id="f5c0e-176">When running in the production environment, the Rails application needs precompiled assets.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-176">When running in the production environment, the Rails application needs precompiled assets.</span></span> <span data-ttu-id="f5c0e-177">Generate the required assets with the following command:</span><span class="sxs-lookup"><span data-stu-id="f5c0e-177">Generate the required assets with the following command:</span></span>

```bash
rake assets:precompile
```

<span data-ttu-id="f5c0e-178">The Rails production environment also uses secrets to manage security.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-178">The Rails production environment also uses secrets to manage security.</span></span> <span data-ttu-id="f5c0e-179">Generate a secret key.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-179">Generate a secret key.</span></span>

```bash
rails secret
```

<span data-ttu-id="f5c0e-180">Save the secret key to the respective variables used by the Rails production environment.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-180">Save the secret key to the respective variables used by the Rails production environment.</span></span> <span data-ttu-id="f5c0e-181">For convenience, you use the same key for both variables.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-181">For convenience, you use the same key for both variables.</span></span>

```bash
export RAILS_MASTER_KEY=<output_of_rails_secret>
export SECRET_KEY_BASE=<output_of_rails_secret>
```

<span data-ttu-id="f5c0e-182">Enable the Rails production environment to serve JavaScript and CSS files.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-182">Enable the Rails production environment to serve JavaScript and CSS files.</span></span>

```bash
export RAILS_SERVE_STATIC_FILES=true
```

<span data-ttu-id="f5c0e-183">Run the sample application in the production environment.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-183">Run the sample application in the production environment.</span></span>

```bash
rails server -e production
```

<span data-ttu-id="f5c0e-184">Navigate to `http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-184">Navigate to `http://localhost:3000`.</span></span> <span data-ttu-id="f5c0e-185">If the page loads without errors, the Ruby on Rails application is connecting to the Postgres database in Azure.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-185">If the page loads without errors, the Ruby on Rails application is connecting to the Postgres database in Azure.</span></span>

<span data-ttu-id="f5c0e-186">Add a few tasks in the page.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-186">Add a few tasks in the page.</span></span>

![Ruby on Rails connects successfully to Azure Database for PostgreSQL](./media/tutorial-ruby-postgres-app/azure-postgres-connect-success.png)

<span data-ttu-id="f5c0e-188">To stop the Rails server, type `Ctrl + C` in the terminal.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-188">To stop the Rails server, type `Ctrl + C` in the terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="f5c0e-189">Commit your changes</span><span class="sxs-lookup"><span data-stu-id="f5c0e-189">Commit your changes</span></span>

<span data-ttu-id="f5c0e-190">Run the following Git commands to commit your changes:</span><span class="sxs-lookup"><span data-stu-id="f5c0e-190">Run the following Git commands to commit your changes:</span></span>

```bash
git add .
git commit -m "database.yml updates"
```

<span data-ttu-id="f5c0e-191">Your app is ready to be deployed.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-191">Your app is ready to be deployed.</span></span>

## <a name="deploy-to-azure"></a><span data-ttu-id="f5c0e-192">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="f5c0e-192">Deploy to Azure</span></span>

<span data-ttu-id="f5c0e-193">In this step, you deploy the Postgres-connected Rails application to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-193">In this step, you deploy the Postgres-connected Rails application to Azure App Service.</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="f5c0e-194">Configure a deployment user</span><span class="sxs-lookup"><span data-stu-id="f5c0e-194">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../../includes/configure-deployment-user-no-h.md)]

### <a name="create-an-app-service-plan"></a><span data-ttu-id="f5c0e-195">Create an App Service plan</span><span class="sxs-lookup"><span data-stu-id="f5c0e-195">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../../includes/app-service-web-create-app-service-plan-linux-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="f5c0e-196">Create a web app</span><span class="sxs-lookup"><span data-stu-id="f5c0e-196">Create a web app</span></span>

[!INCLUDE [Create web app](../../../includes/app-service-web-create-web-app-ruby-linux-no-h.md)] 

### <a name="configure-database-settings"></a><span data-ttu-id="f5c0e-197">Configure database settings</span><span class="sxs-lookup"><span data-stu-id="f5c0e-197">Configure database settings</span></span>

<span data-ttu-id="f5c0e-198">In App Service, you set environment variables as _app settings_ by using the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in the Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-198">In App Service, you set environment variables as _app settings_ by using the [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) command in the Cloud Shell.</span></span>

<span data-ttu-id="f5c0e-199">The following Cloud Shell command configures the app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-199">The following Cloud Shell command configures the app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="f5c0e-200">Replace the placeholders _&lt;appname>_ and _&lt;postgres_server_name>_.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-200">Replace the placeholders _&lt;appname>_ and _&lt;postgres_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DB_HOST="<postgres_server_name>.postgres.database.azure.com" DB_DATABASE="sampledb" DB_USERNAME="railsappuser@<postgres_server_name>" DB_PASSWORD="MyPostgresAzure2017"
```

### <a name="configure-rails-environment-variables"></a><span data-ttu-id="f5c0e-201">Configure Rails environment variables</span><span class="sxs-lookup"><span data-stu-id="f5c0e-201">Configure Rails environment variables</span></span>

<span data-ttu-id="f5c0e-202">In the local terminal, generate a new secret key for the Rails production environment in Azure.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-202">In the local terminal, generate a new secret key for the Rails production environment in Azure.</span></span>

```bash
rails secret
```

<span data-ttu-id="f5c0e-203">Configure the variables required by Rails production environment.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-203">Configure the variables required by Rails production environment.</span></span>

<span data-ttu-id="f5c0e-204">In the following Cloud Shell command, replace the two _&lt;output_of_rails_secret>_ placeholders with the new secret key you generated in the local terminal.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-204">In the following Cloud Shell command, replace the two _&lt;output_of_rails_secret>_ placeholders with the new secret key you generated in the local terminal.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings RAILS_MASTER_KEY="<output_of_rails_secret>" SECRET_KEY_BASE="<output_of_rails_secret>" RAILS_SERVE_STATIC_FILES="true" ASSETS_PRECOMPILE="true"
```

<span data-ttu-id="f5c0e-205">`ASSETS_PRECOMPILE="true"` tells the default Ruby container to precompile assets at each Git deployment.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-205">`ASSETS_PRECOMPILE="true"` tells the default Ruby container to precompile assets at each Git deployment.</span></span>

### <a name="push-to-azure-from-git"></a><span data-ttu-id="f5c0e-206">Push to Azure from Git</span><span class="sxs-lookup"><span data-stu-id="f5c0e-206">Push to Azure from Git</span></span>

<span data-ttu-id="f5c0e-207">In the local terminal, add an Azure remote to your local Git repository.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-207">In the local terminal, add an Azure remote to your local Git repository.</span></span>

```bash
git remote add azure <paste_copied_url_here>
```

<span data-ttu-id="f5c0e-208">Push to the Azure remote to deploy the Ruby on Rails application.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-208">Push to the Azure remote to deploy the Ruby on Rails application.</span></span> <span data-ttu-id="f5c0e-209">You are prompted for the password you supplied earlier as part of the creation of the deployment user.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-209">You are prompted for the password you supplied earlier as part of the creation of the deployment user.</span></span>

```bash
git push azure master
```

<span data-ttu-id="f5c0e-210">During deployment, Azure App Service communicates its progress with Git.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-210">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'a5e076db9c'.
remote: Running custom deployment command...
remote: Running deployment command...
...
< Output has been truncated for readability >
```

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="f5c0e-211">Browse to the Azure web app</span><span class="sxs-lookup"><span data-stu-id="f5c0e-211">Browse to the Azure web app</span></span>

<span data-ttu-id="f5c0e-212">Browse to `http://<app_name>.azurewebsites.net` and add a few tasks to the list.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-212">Browse to `http://<app_name>.azurewebsites.net` and add a few tasks to the list.</span></span>

![Ruby on Rails app running in Azure App Service](./media/tutorial-ruby-postgres-app/ruby-postgres-in-azure.png)

<span data-ttu-id="f5c0e-214">Congratulations, you're running a data-driven Ruby on Rails app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-214">Congratulations, you're running a data-driven Ruby on Rails app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="f5c0e-215">Update model locally and redeploy</span><span class="sxs-lookup"><span data-stu-id="f5c0e-215">Update model locally and redeploy</span></span>

<span data-ttu-id="f5c0e-216">In this step, you make a simple change to the `task` data model and the webapp, and then publish the update to Azure.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-216">In this step, you make a simple change to the `task` data model and the webapp, and then publish the update to Azure.</span></span>

<span data-ttu-id="f5c0e-217">For the tasks scenario, you modify the application so that you can mark a task as complete.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-217">For the tasks scenario, you modify the application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="f5c0e-218">Add a column</span><span class="sxs-lookup"><span data-stu-id="f5c0e-218">Add a column</span></span>

<span data-ttu-id="f5c0e-219">In the terminal, navigate to the root of the Git repository.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-219">In the terminal, navigate to the root of the Git repository.</span></span>

<span data-ttu-id="f5c0e-220">Generate a new migration that adds a boolean column called `Done` to the `Tasks` table:</span><span class="sxs-lookup"><span data-stu-id="f5c0e-220">Generate a new migration that adds a boolean column called `Done` to the `Tasks` table:</span></span>

```bash
rails generate migration AddDoneToTasks Done:boolean
```

<span data-ttu-id="f5c0e-221">This command generates a new migration file in the _db/migrate_ directory.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-221">This command generates a new migration file in the _db/migrate_ directory.</span></span>


<span data-ttu-id="f5c0e-222">In the terminal, run Rails database migrations to make the change in the local database.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-222">In the terminal, run Rails database migrations to make the change in the local database.</span></span>

```bash
rake db:migrate
```

### <a name="update-application-logic"></a><span data-ttu-id="f5c0e-223">Update application logic</span><span class="sxs-lookup"><span data-stu-id="f5c0e-223">Update application logic</span></span>

<span data-ttu-id="f5c0e-224">Open the *app/controllers/tasks_controller.rb* file.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-224">Open the *app/controllers/tasks_controller.rb* file.</span></span> <span data-ttu-id="f5c0e-225">At the end of the file, find the following line:</span><span class="sxs-lookup"><span data-stu-id="f5c0e-225">At the end of the file, find the following line:</span></span>

```rb
params.require(:task).permit(:Description)
```

<span data-ttu-id="f5c0e-226">Modify this line to include the new `Done` parameter.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-226">Modify this line to include the new `Done` parameter.</span></span>

```rb
params.require(:task).permit(:Description, :Done)
```

### <a name="update-the-views"></a><span data-ttu-id="f5c0e-227">Update the views</span><span class="sxs-lookup"><span data-stu-id="f5c0e-227">Update the views</span></span>

<span data-ttu-id="f5c0e-228">Open the *app/views/tasks/_form.html.erb* file, which is the Edit form.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-228">Open the *app/views/tasks/_form.html.erb* file, which is the Edit form.</span></span>

<span data-ttu-id="f5c0e-229">Find the line `<%=f.error_span(:Description) %>` and insert the following code directly below it:</span><span class="sxs-lookup"><span data-stu-id="f5c0e-229">Find the line `<%=f.error_span(:Description) %>` and insert the following code directly below it:</span></span>

```erb
<%= f.label :Done, :class => 'control-label col-lg-2' %>
<div class="col-lg-10">
  <%= f.check_box :Done, :class => 'form-control' %>
</div>
```

<span data-ttu-id="f5c0e-230">Open the *app/views/tasks/show.html.erb* file, which is the single-record View page.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-230">Open the *app/views/tasks/show.html.erb* file, which is the single-record View page.</span></span> 

<span data-ttu-id="f5c0e-231">Find the line `<dd><%= @task.Description %></dd>` and insert the following code directly below it:</span><span class="sxs-lookup"><span data-stu-id="f5c0e-231">Find the line `<dd><%= @task.Description %></dd>` and insert the following code directly below it:</span></span>

```erb
  <dt><strong><%= model_class.human_attribute_name(:Done) %>:</strong></dt>
  <dd><%= check_box "task", "Done", {:checked => @task.Done, :disabled => true}%></dd>
```

<span data-ttu-id="f5c0e-232">Open the *app/views/tasks/index.html.erb* file, which is the Index page for all records.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-232">Open the *app/views/tasks/index.html.erb* file, which is the Index page for all records.</span></span>

<span data-ttu-id="f5c0e-233">Find the line `<th><%= model_class.human_attribute_name(:Description) %></th>` and insert the following code directly below it:</span><span class="sxs-lookup"><span data-stu-id="f5c0e-233">Find the line `<th><%= model_class.human_attribute_name(:Description) %></th>` and insert the following code directly below it:</span></span>

```erb
<th><%= model_class.human_attribute_name(:Done) %></th>
```

<span data-ttu-id="f5c0e-234">In the same file, find the line `<td><%= task.Description %></td>` and insert the following code directly below it:</span><span class="sxs-lookup"><span data-stu-id="f5c0e-234">In the same file, find the line `<td><%= task.Description %></td>` and insert the following code directly below it:</span></span>

```erb
<td><%= check_box "task", "Done", {:checked => task.Done, :disabled => true} %></td>
```

### <a name="test-the-changes-locally"></a><span data-ttu-id="f5c0e-235">Test the changes locally</span><span class="sxs-lookup"><span data-stu-id="f5c0e-235">Test the changes locally</span></span>

<span data-ttu-id="f5c0e-236">In the local terminal, run the Rails server.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-236">In the local terminal, run the Rails server.</span></span>

```bash
rails server
```

<span data-ttu-id="f5c0e-237">To see the task status change, navigate to `http://localhost:3000` and add or edit items.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-237">To see the task status change, navigate to `http://localhost:3000` and add or edit items.</span></span>

![Added check box to task](./media/tutorial-ruby-postgres-app/complete-checkbox.png)

<span data-ttu-id="f5c0e-239">To stop the Rails server, type `Ctrl + C` in the terminal.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-239">To stop the Rails server, type `Ctrl + C` in the terminal.</span></span>

### <a name="publish-changes-to-azure"></a><span data-ttu-id="f5c0e-240">Publish changes to Azure</span><span class="sxs-lookup"><span data-stu-id="f5c0e-240">Publish changes to Azure</span></span>

<span data-ttu-id="f5c0e-241">In the terminal, run Rails database migrations for the production environment to make the change in the Azure database.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-241">In the terminal, run Rails database migrations for the production environment to make the change in the Azure database.</span></span>

```bash
rake db:migrate RAILS_ENV=production
```

<span data-ttu-id="f5c0e-242">Commit all the changes in Git, and then push the code changes to Azure.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-242">Commit all the changes in Git, and then push the code changes to Azure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="f5c0e-243">Once the `git push` is complete, navigate to the Azure web app and test the new functionality.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-243">Once the `git push` is complete, navigate to the Azure web app and test the new functionality.</span></span>

![Model and database changes published to Azure](media/tutorial-ruby-postgres-app/complete-checkbox-published.png)

<span data-ttu-id="f5c0e-245">If you added any tasks, they are retained in the database.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-245">If you added any tasks, they are retained in the database.</span></span> <span data-ttu-id="f5c0e-246">Updates to the data schema leave existing data intact.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-246">Updates to the data schema leave existing data intact.</span></span>

## <a name="manage-the-azure-web-app"></a><span data-ttu-id="f5c0e-247">Manage the Azure web app</span><span class="sxs-lookup"><span data-stu-id="f5c0e-247">Manage the Azure web app</span></span>

<span data-ttu-id="f5c0e-248">Go to the [Azure portal](https://portal.azure.com) to manage the web app you created.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-248">Go to the [Azure portal](https://portal.azure.com) to manage the web app you created.</span></span>

<span data-ttu-id="f5c0e-249">From the left menu, click **App Services**, and then click the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-249">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](./media/tutorial-php-mysql-app/access-portal.png)

<span data-ttu-id="f5c0e-251">You see your web app's Overview page.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-251">You see your web app's Overview page.</span></span> <span data-ttu-id="f5c0e-252">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-252">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="f5c0e-253">The left menu provides pages for configuring your app.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-253">The left menu provides pages for configuring your app.</span></span>

![App Service page in Azure portal](./media/tutorial-php-mysql-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="f5c0e-255">Next steps</span><span class="sxs-lookup"><span data-stu-id="f5c0e-255">Next steps</span></span>

<span data-ttu-id="f5c0e-256">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="f5c0e-256">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f5c0e-257">Create a Postgres database in Azure</span><span class="sxs-lookup"><span data-stu-id="f5c0e-257">Create a Postgres database in Azure</span></span>
> * <span data-ttu-id="f5c0e-258">Connect a Ruby on Rails app to Postgres</span><span class="sxs-lookup"><span data-stu-id="f5c0e-258">Connect a Ruby on Rails app to Postgres</span></span>
> * <span data-ttu-id="f5c0e-259">Deploy the app to Azure</span><span class="sxs-lookup"><span data-stu-id="f5c0e-259">Deploy the app to Azure</span></span>
> * <span data-ttu-id="f5c0e-260">Update the data model and redeploy the app</span><span class="sxs-lookup"><span data-stu-id="f5c0e-260">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="f5c0e-261">Stream diagnostic logs from Azure</span><span class="sxs-lookup"><span data-stu-id="f5c0e-261">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="f5c0e-262">Manage the app in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f5c0e-262">Manage the app in the Azure portal</span></span>

<span data-ttu-id="f5c0e-263">Advance to the next tutorial to learn how to map a custom DNS name to a web app.</span><span class="sxs-lookup"><span data-stu-id="f5c0e-263">Advance to the next tutorial to learn how to map a custom DNS name to a web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f5c0e-264">Map an existing custom DNS name to Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="f5c0e-264">Map an existing custom DNS name to Azure Web Apps</span></span>](../app-service-web-tutorial-custom-domain.md)
