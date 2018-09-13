<span data-ttu-id="a4548-101">The storage emulator supports a single fixed account and a well-known authentication key for Shared Key authentication.</span><span class="sxs-lookup"><span data-stu-id="a4548-101">The storage emulator supports a single fixed account and a well-known authentication key for Shared Key authentication.</span></span> <span data-ttu-id="a4548-102">This account and key are the only Shared Key credentials permitted for use with the storage emulator.</span><span class="sxs-lookup"><span data-stu-id="a4548-102">This account and key are the only Shared Key credentials permitted for use with the storage emulator.</span></span> <span data-ttu-id="a4548-103">They are:</span><span class="sxs-lookup"><span data-stu-id="a4548-103">They are:</span></span>

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> <span data-ttu-id="a4548-104">The authentication key supported by the storage emulator is intended only for testing the functionality of your client authentication code.</span><span class="sxs-lookup"><span data-stu-id="a4548-104">The authentication key supported by the storage emulator is intended only for testing the functionality of your client authentication code.</span></span> <span data-ttu-id="a4548-105">It does not serve any security purpose.</span><span class="sxs-lookup"><span data-stu-id="a4548-105">It does not serve any security purpose.</span></span> <span data-ttu-id="a4548-106">You cannot use your production storage account and key with the storage emulator.</span><span class="sxs-lookup"><span data-stu-id="a4548-106">You cannot use your production storage account and key with the storage emulator.</span></span> <span data-ttu-id="a4548-107">You should not use the development account with production data.</span><span class="sxs-lookup"><span data-stu-id="a4548-107">You should not use the development account with production data.</span></span>
> 
> <span data-ttu-id="a4548-108">The storage emulator supports connection via HTTP only.</span><span class="sxs-lookup"><span data-stu-id="a4548-108">The storage emulator supports connection via HTTP only.</span></span> <span data-ttu-id="a4548-109">However, HTTPS is the recommended protocol for accessing resources in a production Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="a4548-109">However, HTTPS is the recommended protocol for accessing resources in a production Azure storage account.</span></span>
> 

#### <a name="connect-to-the-emulator-account-using-a-shortcut"></a><span data-ttu-id="a4548-110">Connect to the emulator account using a shortcut</span><span class="sxs-lookup"><span data-stu-id="a4548-110">Connect to the emulator account using a shortcut</span></span>
<span data-ttu-id="a4548-111">The easiest way to connect to the storage emulator from your application is to configure a connection string in your application's configuration file that references the shortcut `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="a4548-111">The easiest way to connect to the storage emulator from your application is to configure a connection string in your application's configuration file that references the shortcut `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="a4548-112">Here's an example of a connection string to the storage emulator in an *app.config* file:</span><span class="sxs-lookup"><span data-stu-id="a4548-112">Here's an example of a connection string to the storage emulator in an *app.config* file:</span></span> 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-to-the-emulator-account-using-the-well-known-account-name-and-key"></a><span data-ttu-id="a4548-113">Connect to the emulator account using the well-known account name and key</span><span class="sxs-lookup"><span data-stu-id="a4548-113">Connect to the emulator account using the well-known account name and key</span></span>
<span data-ttu-id="a4548-114">To create a connection string that references the emulator account name and key, you must specify the endpoints for each of the services you wish to use from the emulator in the connection string.</span><span class="sxs-lookup"><span data-stu-id="a4548-114">To create a connection string that references the emulator account name and key, you must specify the endpoints for each of the services you wish to use from the emulator in the connection string.</span></span> <span data-ttu-id="a4548-115">This is necessary so that the connection string will reference the emulator endpoints, which are different than those for a production storage account.</span><span class="sxs-lookup"><span data-stu-id="a4548-115">This is necessary so that the connection string will reference the emulator endpoints, which are different than those for a production storage account.</span></span> <span data-ttu-id="a4548-116">For example, the value of your connection string will look like this:</span><span class="sxs-lookup"><span data-stu-id="a4548-116">For example, the value of your connection string will look like this:</span></span>

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

<span data-ttu-id="a4548-117">This value is identical to the shortcut shown above, `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="a4548-117">This value is identical to the shortcut shown above, `UseDevelopmentStorage=true`.</span></span>

#### <a name="specify-an-http-proxy"></a><span data-ttu-id="a4548-118">Specify an HTTP proxy</span><span class="sxs-lookup"><span data-stu-id="a4548-118">Specify an HTTP proxy</span></span>
<span data-ttu-id="a4548-119">You can also specify an HTTP proxy to use when you're testing your service against the storage emulator.</span><span class="sxs-lookup"><span data-stu-id="a4548-119">You can also specify an HTTP proxy to use when you're testing your service against the storage emulator.</span></span> <span data-ttu-id="a4548-120">This can be useful for observing HTTP requests and responses while you're debugging operations against the storage services.</span><span class="sxs-lookup"><span data-stu-id="a4548-120">This can be useful for observing HTTP requests and responses while you're debugging operations against the storage services.</span></span> <span data-ttu-id="a4548-121">To specify a proxy, add the `DevelopmentStorageProxyUri` option to the connection string, and set its value to the proxy URI.</span><span class="sxs-lookup"><span data-stu-id="a4548-121">To specify a proxy, add the `DevelopmentStorageProxyUri` option to the connection string, and set its value to the proxy URI.</span></span> <span data-ttu-id="a4548-122">For example, here is a connection string that points to the storage emulator and configures an HTTP proxy:</span><span class="sxs-lookup"><span data-stu-id="a4548-122">For example, here is a connection string that points to the storage emulator and configures an HTTP proxy:</span></span>

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

