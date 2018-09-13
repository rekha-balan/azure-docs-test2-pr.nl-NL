<span data-ttu-id="dfd51-101">The [Microsoft Azure Configuration Manager Library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) provides a class for parsing a connection string from a configuration file.</span><span class="sxs-lookup"><span data-stu-id="dfd51-101">The [Microsoft Azure Configuration Manager Library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) provides a class for parsing a connection string from a configuration file.</span></span> <span data-ttu-id="dfd51-102">The [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) class parses configuration settings regardless of whether the client application is running on the desktop, on a mobile device, in an Azure virtual machine, or in an Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="dfd51-102">The [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) class parses configuration settings regardless of whether the client application is running on the desktop, on a mobile device, in an Azure virtual machine, or in an Azure cloud service.</span></span>

<span data-ttu-id="dfd51-103">To reference the CloudConfigurationManager package, add the following `using` directive:</span><span class="sxs-lookup"><span data-stu-id="dfd51-103">To reference the CloudConfigurationManager package, add the following `using` directive:</span></span>

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

<span data-ttu-id="dfd51-104">Here's an example that shows how to retrieve a connection string from a configuration file:</span><span class="sxs-lookup"><span data-stu-id="dfd51-104">Here's an example that shows how to retrieve a connection string from a configuration file:</span></span>

```csharp
// Parse the connection string and return a reference to the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

<span data-ttu-id="dfd51-105">Using the Azure Configuration Manager is optional.</span><span class="sxs-lookup"><span data-stu-id="dfd51-105">Using the Azure Configuration Manager is optional.</span></span> <span data-ttu-id="dfd51-106">You can also use an API like the .NET Framework's [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) class.</span><span class="sxs-lookup"><span data-stu-id="dfd51-106">You can also use an API like the .NET Framework's [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) class.</span></span>

