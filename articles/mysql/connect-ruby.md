---
title: Connect to Azure Database for MySQL using Ruby
description: This quickstart provides several Ruby code samples you can use to connect and query data from Azure Database for MySQL.
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.custom: mvc
ms.devlang: ruby
ms.topic: quickstart
ms.date: 02/28/2018
ms.openlocfilehash: cbd60be37dc7021ecbb961027dca40d048ed84cb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855726"
---
# <a name="azure-database-for-mysql-use-ruby-to-connect-and-query-data"></a><span data-ttu-id="0ef50-103">Azure Database for MySQL: Use Ruby to connect and query data</span><span class="sxs-lookup"><span data-stu-id="0ef50-103">Azure Database for MySQL: Use Ruby to connect and query data</span></span>
<span data-ttu-id="0ef50-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a [Ruby](https://www.ruby-lang.org) application and the [mysql2](https://rubygems.org/gems/mysql2) gem from Windows, Ubuntu Linux, and Mac platforms.</span><span class="sxs-lookup"><span data-stu-id="0ef50-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a [Ruby](https://www.ruby-lang.org) application and the [mysql2](https://rubygems.org/gems/mysql2) gem from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="0ef50-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span><span class="sxs-lookup"><span data-stu-id="0ef50-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="0ef50-106">This topic assumes that you are familiar with development using Ruby and that you are new to working with Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="0ef50-106">This topic assumes that you are familiar with development using Ruby and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ef50-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0ef50-107">Prerequisites</span></span>
<span data-ttu-id="0ef50-108">This quickstart uses the resources created in either of these guides as a starting point:</span><span class="sxs-lookup"><span data-stu-id="0ef50-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="0ef50-109">Create an Azure Database for MySQL server using Azure portal</span><span class="sxs-lookup"><span data-stu-id="0ef50-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="0ef50-110">Create an Azure Database for MySQL server using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0ef50-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="0ef50-111">Install Ruby</span><span class="sxs-lookup"><span data-stu-id="0ef50-111">Install Ruby</span></span>
<span data-ttu-id="0ef50-112">Install Ruby, Gem, and the MySQL2 library on your own computer.</span><span class="sxs-lookup"><span data-stu-id="0ef50-112">Install Ruby, Gem, and the MySQL2 library on your own computer.</span></span> 

### <a name="windows"></a><span data-ttu-id="0ef50-113">Windows</span><span class="sxs-lookup"><span data-stu-id="0ef50-113">Windows</span></span>
1. <span data-ttu-id="0ef50-114">Download and Install the 2.3 version of [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="0ef50-114">Download and Install the 2.3 version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
2. <span data-ttu-id="0ef50-115">Launch a new command prompt (cmd) from the Start menu.</span><span class="sxs-lookup"><span data-stu-id="0ef50-115">Launch a new command prompt (cmd) from the Start menu.</span></span>
3. <span data-ttu-id="0ef50-116">Change directory into the Ruby directory for version 2.3.</span><span class="sxs-lookup"><span data-stu-id="0ef50-116">Change directory into the Ruby directory for version 2.3.</span></span> `cd c:\Ruby23-x64\bin`
4. <span data-ttu-id="0ef50-117">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span><span class="sxs-lookup"><span data-stu-id="0ef50-117">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
5. <span data-ttu-id="0ef50-118">Test the Gem installation by running the command `gem -v` to see the version installed.</span><span class="sxs-lookup"><span data-stu-id="0ef50-118">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
6. <span data-ttu-id="0ef50-119">Build the Mysql2 module for Ruby using Gem by running the command `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="0ef50-119">Build the Mysql2 module for Ruby using Gem by running the command `gem install mysql2`.</span></span>

### <a name="macos"></a><span data-ttu-id="0ef50-120">MacOS</span><span class="sxs-lookup"><span data-stu-id="0ef50-120">MacOS</span></span>
1. <span data-ttu-id="0ef50-121">Install Ruby using Homebrew by running the command `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="0ef50-121">Install Ruby using Homebrew by running the command `brew install ruby`.</span></span> <span data-ttu-id="0ef50-122">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span><span class="sxs-lookup"><span data-stu-id="0ef50-122">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span></span>
2. <span data-ttu-id="0ef50-123">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span><span class="sxs-lookup"><span data-stu-id="0ef50-123">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
3. <span data-ttu-id="0ef50-124">Test the Gem installation by running the command `gem -v` to see the version installed.</span><span class="sxs-lookup"><span data-stu-id="0ef50-124">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
4. <span data-ttu-id="0ef50-125">Build the Mysql2 module for Ruby using Gem by running the command `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="0ef50-125">Build the Mysql2 module for Ruby using Gem by running the command `gem install mysql2`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="0ef50-126">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="0ef50-126">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="0ef50-127">Install Ruby by running the command `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="0ef50-127">Install Ruby by running the command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="0ef50-128">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span><span class="sxs-lookup"><span data-stu-id="0ef50-128">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
2. <span data-ttu-id="0ef50-129">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span><span class="sxs-lookup"><span data-stu-id="0ef50-129">Test the Ruby installation by running the command `ruby -v` to see the version installed.</span></span>
3. <span data-ttu-id="0ef50-130">Install the latest updates for Gem by running the command `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="0ef50-130">Install the latest updates for Gem by running the command `sudo gem update --system`.</span></span>
4. <span data-ttu-id="0ef50-131">Test the Gem installation by running the command `gem -v` to see the version installed.</span><span class="sxs-lookup"><span data-stu-id="0ef50-131">Test the Gem installation by running the command `gem -v` to see the version installed.</span></span>
5. <span data-ttu-id="0ef50-132">Install the gcc, make, and other build tools by running the command `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="0ef50-132">Install the gcc, make, and other build tools by running the command `sudo apt-get install build-essential`.</span></span>
6. <span data-ttu-id="0ef50-133">Install the MySQL client developer libraries by running the command `sudo apt-get install libmysqlclient-dev`.</span><span class="sxs-lookup"><span data-stu-id="0ef50-133">Install the MySQL client developer libraries by running the command `sudo apt-get install libmysqlclient-dev`.</span></span>
7. <span data-ttu-id="0ef50-134">Build the mysql2 module for Ruby using Gem by running the command `sudo gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="0ef50-134">Build the mysql2 module for Ruby using Gem by running the command `sudo gem install mysql2`.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="0ef50-135">Get connection information</span><span class="sxs-lookup"><span data-stu-id="0ef50-135">Get connection information</span></span>
<span data-ttu-id="0ef50-136">Get the connection information needed to connect to the Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="0ef50-136">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="0ef50-137">You need the fully qualified server name and login credentials.</span><span class="sxs-lookup"><span data-stu-id="0ef50-137">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="0ef50-138">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0ef50-138">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0ef50-139">From the left-hand menu in Azure portal, click **All resources**, and then search for the server you have created (such as **mydemoserver**).</span><span class="sxs-lookup"><span data-stu-id="0ef50-139">From the left-hand menu in Azure portal, click **All resources**, and then search for the server you have created (such as **mydemoserver**).</span></span>
3. <span data-ttu-id="0ef50-140">Click the server name.</span><span class="sxs-lookup"><span data-stu-id="0ef50-140">Click the server name.</span></span>
4. <span data-ttu-id="0ef50-141">From the server's **Overview** panel, make a note of the **Server name** and **Server admin login name**.</span><span class="sxs-lookup"><span data-stu-id="0ef50-141">From the server's **Overview** panel, make a note of the **Server name** and **Server admin login name**.</span></span> <span data-ttu-id="0ef50-142">If you forget your password, you can also reset the password from this panel.</span><span class="sxs-lookup"><span data-stu-id="0ef50-142">If you forget your password, you can also reset the password from this panel.</span></span>
 <span data-ttu-id="0ef50-143">![Azure Database for MySQL server name](./media/connect-ruby/1_server-overview-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="0ef50-143">![Azure Database for MySQL server name](./media/connect-ruby/1_server-overview-name-login.png)</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="0ef50-144">Run Ruby code</span><span class="sxs-lookup"><span data-stu-id="0ef50-144">Run Ruby code</span></span> 
1. <span data-ttu-id="0ef50-145">Paste the Ruby code from the sections below into text files, and then save the files into a project folder with file extension .rb (such as `C:\rubymysql\createtable.rb` or `/home/username/rubymysql/createtable.rb`).</span><span class="sxs-lookup"><span data-stu-id="0ef50-145">Paste the Ruby code from the sections below into text files, and then save the files into a project folder with file extension .rb (such as `C:\rubymysql\createtable.rb` or `/home/username/rubymysql/createtable.rb`).</span></span>
2. <span data-ttu-id="0ef50-146">To run the code, launch the command prompt or Bash shell.</span><span class="sxs-lookup"><span data-stu-id="0ef50-146">To run the code, launch the command prompt or Bash shell.</span></span> <span data-ttu-id="0ef50-147">Change directory into your project folder `cd rubymysql`</span><span class="sxs-lookup"><span data-stu-id="0ef50-147">Change directory into your project folder `cd rubymysql`</span></span>
3. <span data-ttu-id="0ef50-148">Then type the Ruby command followed by the file name, such as `ruby createtable.rb` to run the application.</span><span class="sxs-lookup"><span data-stu-id="0ef50-148">Then type the Ruby command followed by the file name, such as `ruby createtable.rb` to run the application.</span></span>
4. <span data-ttu-id="0ef50-149">On the Windows OS, if the Ruby application is not in your path environment variable, you may need to use the full path to launch the node application, such as `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span><span class="sxs-lookup"><span data-stu-id="0ef50-149">On the Windows OS, if the Ruby application is not in your path environment variable, you may need to use the full path to launch the node application, such as `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="0ef50-150">Connect and create a table</span><span class="sxs-lookup"><span data-stu-id="0ef50-150">Connect and create a table</span></span>
<span data-ttu-id="0ef50-151">Use the following code to connect and create a table by using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span><span class="sxs-lookup"><span data-stu-id="0ef50-151">Use the following code to connect and create a table by using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="0ef50-152">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="0ef50-152">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="0ef50-153">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) several times to run the DROP, CREATE TABLE, and INSERT INTO commands.</span><span class="sxs-lookup"><span data-stu-id="0ef50-153">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) several times to run the DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="0ef50-154">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span><span class="sxs-lookup"><span data-stu-id="0ef50-154">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="0ef50-155">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span><span class="sxs-lookup"><span data-stu-id="0ef50-155">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 
```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('mydemoserver.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@mydemoserver')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection to database.'

    # Drop previous table of same name if one exists
    client.query('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    client.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    client.query("INSERT INTO inventory VALUES(1, 'banana', 150)")
    client.query("INSERT INTO inventory VALUES(2, 'orange', 154)")
    client.query("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="read-data"></a><span data-ttu-id="0ef50-156">Read data</span><span class="sxs-lookup"><span data-stu-id="0ef50-156">Read data</span></span>
<span data-ttu-id="0ef50-157">Use the following code to connect and read the data by using a **SELECT** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="0ef50-157">Use the following code to connect and read the data by using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="0ef50-158">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class.new() method to connect to Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="0ef50-158">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class.new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="0ef50-159">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the SELECT commands.</span><span class="sxs-lookup"><span data-stu-id="0ef50-159">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the SELECT commands.</span></span> <span data-ttu-id="0ef50-160">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span><span class="sxs-lookup"><span data-stu-id="0ef50-160">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="0ef50-161">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span><span class="sxs-lookup"><span data-stu-id="0ef50-161">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('mydemoserver.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@mydemoserver')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection to database.'

    # Read data
    resultSet = client.query('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end
    puts 'Read ' + resultSet.count.to_s + ' row(s).'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="update-data"></a><span data-ttu-id="0ef50-162">Update data</span><span class="sxs-lookup"><span data-stu-id="0ef50-162">Update data</span></span>
<span data-ttu-id="0ef50-163">Use the following code to connect and update the data by using an **UPDATE** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="0ef50-163">Use the following code to connect and update the data by using an **UPDATE** SQL statement.</span></span>

<span data-ttu-id="0ef50-164">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="0ef50-164">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="0ef50-165">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the UPDATE commands.</span><span class="sxs-lookup"><span data-stu-id="0ef50-165">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the UPDATE commands.</span></span> <span data-ttu-id="0ef50-166">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span><span class="sxs-lookup"><span data-stu-id="0ef50-166">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="0ef50-167">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span><span class="sxs-lookup"><span data-stu-id="0ef50-167">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('mydemoserver.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@mydemoserver')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection to database.'

    # Update data
   client.query('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
   puts 'Updated 1 row of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```


## <a name="delete-data"></a><span data-ttu-id="0ef50-168">Delete data</span><span class="sxs-lookup"><span data-stu-id="0ef50-168">Delete data</span></span>
<span data-ttu-id="0ef50-169">Use the following code to connect and read the data by using a **DELETE** SQL statement.</span><span class="sxs-lookup"><span data-stu-id="0ef50-169">Use the following code to connect and read the data by using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="0ef50-170">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="0ef50-170">The code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="0ef50-171">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the DELETE commands.</span><span class="sxs-lookup"><span data-stu-id="0ef50-171">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) to run the DELETE commands.</span></span> <span data-ttu-id="0ef50-172">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span><span class="sxs-lookup"><span data-stu-id="0ef50-172">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="0ef50-173">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span><span class="sxs-lookup"><span data-stu-id="0ef50-173">Replace the `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('mydemoserver.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@mydemoserver')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection to database.'

    # Delete data
    resultSet = client.query('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="next-steps"></a><span data-ttu-id="0ef50-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="0ef50-174">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="0ef50-175">Migrate your database using Export and Import</span><span class="sxs-lookup"><span data-stu-id="0ef50-175">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
