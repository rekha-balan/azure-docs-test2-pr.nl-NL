---
title: Connecting to Media Services Account using .NET
description: This topic demonstrates how to connect to Media Services uisng .NET.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: a8412a29-59dc-44a0-ace0-be79a97dab63
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 892932116934952265a21ab17aac3434b5760136
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661315"
---
# <a name="connecting-to-media-services-account-using-media-services-sdk-for-net"></a><span data-ttu-id="86a49-103">Connecting to Media Services Account using Media Services SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="86a49-103">Connecting to Media Services Account using Media Services SDK for .NET</span></span>
> [!div class="op_single_selector"]
> * [REST](media-services-rest-connect-programmatically.md)
> * [.NET](media-services-dotnet-connect-programmatically.md)
> 
> 

<span data-ttu-id="86a49-106">This topic describes how to obtain a programmatic connection to Microsoft Azure Media Services when you are programming with the Media Services SDK for .NET.</span><span class="sxs-lookup"><span data-stu-id="86a49-106">This topic describes how to obtain a programmatic connection to Microsoft Azure Media Services when you are programming with the Media Services SDK for .NET.</span></span>

## <a name="connecting-to-media-services"></a><span data-ttu-id="86a49-107">Connecting to Media Services</span><span class="sxs-lookup"><span data-stu-id="86a49-107">Connecting to Media Services</span></span>
<span data-ttu-id="86a49-108">To connect to Media Services programmatically, you must have previously set up an Azure account, configured Media Services on that account, and then set up a Visual Studio project for development with the Media Services SDK for .NET.</span><span class="sxs-lookup"><span data-stu-id="86a49-108">To connect to Media Services programmatically, you must have previously set up an Azure account, configured Media Services on that account, and then set up a Visual Studio project for development with the Media Services SDK for .NET.</span></span> <span data-ttu-id="86a49-109">For more information, see Setup for Development with the Media Services SDK for .NET.</span><span class="sxs-lookup"><span data-stu-id="86a49-109">For more information, see Setup for Development with the Media Services SDK for .NET.</span></span>

<span data-ttu-id="86a49-110">At the end of the Media Services account setup process, you obtained the following required connection values.</span><span class="sxs-lookup"><span data-stu-id="86a49-110">At the end of the Media Services account setup process, you obtained the following required connection values.</span></span> <span data-ttu-id="86a49-111">Use these to make programmatic connections to Media Services.</span><span class="sxs-lookup"><span data-stu-id="86a49-111">Use these to make programmatic connections to Media Services.</span></span>

* <span data-ttu-id="86a49-112">Your Media Services account name.</span><span class="sxs-lookup"><span data-stu-id="86a49-112">Your Media Services account name.</span></span>
* <span data-ttu-id="86a49-113">Your Media Services account key.</span><span class="sxs-lookup"><span data-stu-id="86a49-113">Your Media Services account key.</span></span>

<span data-ttu-id="86a49-114">To find these values, go to the Azure Managment Portal, select your Media Service account, and click on the “**MANAGE KEYS**” icon on the bottom of the portal window.</span><span class="sxs-lookup"><span data-stu-id="86a49-114">To find these values, go to the Azure Managment Portal, select your Media Service account, and click on the “**MANAGE KEYS**” icon on the bottom of the portal window.</span></span> <span data-ttu-id="86a49-115">Clicking on the icon next to each text box copies the value to the system clipboard.</span><span class="sxs-lookup"><span data-stu-id="86a49-115">Clicking on the icon next to each text box copies the value to the system clipboard.</span></span>

## <a name="creating-a-cloudmediacontext-instance"></a><span data-ttu-id="86a49-116">Creating a CloudMediaContext Instance</span><span class="sxs-lookup"><span data-stu-id="86a49-116">Creating a CloudMediaContext Instance</span></span>
<span data-ttu-id="86a49-117">To start programming against Media Services you need to create a **CloudMediaContext** instance that represents the server context.</span><span class="sxs-lookup"><span data-stu-id="86a49-117">To start programming against Media Services you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="86a49-118">The **CloudMediaContext** includes references to important collections including jobs, assets, files, access policies, and locators.</span><span class="sxs-lookup"><span data-stu-id="86a49-118">The **CloudMediaContext** includes references to important collections including jobs, assets, files, access policies, and locators.</span></span>

> [!NOTE]
> The **CloudMediaContext** class is not thread safe. You should create a new CloudMediaContext per thread or per set of operations.
> 
> 

<span data-ttu-id="86a49-121">CloudMediaContext has five constructor overloads.</span><span class="sxs-lookup"><span data-stu-id="86a49-121">CloudMediaContext has five constructor overloads.</span></span> <span data-ttu-id="86a49-122">It is recommended to use constructors that take **MediaServicesCredentials** as a parameter.</span><span class="sxs-lookup"><span data-stu-id="86a49-122">It is recommended to use constructors that take **MediaServicesCredentials** as a parameter.</span></span> <span data-ttu-id="86a49-123">For more information, see the **Reusing Access Control Service Tokens** that follows.</span><span class="sxs-lookup"><span data-stu-id="86a49-123">For more information, see the **Reusing Access Control Service Tokens** that follows.</span></span> 

<span data-ttu-id="86a49-124">The following example uses the public CloudMediaContext(MediaServicesCredentials credentials) constructor:</span><span class="sxs-lookup"><span data-stu-id="86a49-124">The following example uses the public CloudMediaContext(MediaServicesCredentials credentials) constructor:</span></span>

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a><span data-ttu-id="86a49-125">Reusing Access Control Service Tokens</span><span class="sxs-lookup"><span data-stu-id="86a49-125">Reusing Access Control Service Tokens</span></span>
<span data-ttu-id="86a49-126">This section shows how to reuse Access Control Service tokens by using CloudMediaContext constructors that take MediaServicesCredentials as a parameter.</span><span class="sxs-lookup"><span data-stu-id="86a49-126">This section shows how to reuse Access Control Service tokens by using CloudMediaContext constructors that take MediaServicesCredentials as a parameter.</span></span>

<span data-ttu-id="86a49-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (also known as Access Control Service or ACS) is a cloud-based service that provides an easy way of authenticating and authorizing users to gain access to their web applications.</span><span class="sxs-lookup"><span data-stu-id="86a49-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (also known as Access Control Service or ACS) is a cloud-based service that provides an easy way of authenticating and authorizing users to gain access to their web applications.</span></span> <span data-ttu-id="86a49-128">Microsoft Azure Media Services controls access to its services though OAuth protocol that requires an ACS token.</span><span class="sxs-lookup"><span data-stu-id="86a49-128">Microsoft Azure Media Services controls access to its services though OAuth protocol that requires an ACS token.</span></span> <span data-ttu-id="86a49-129">Media Services receives the ACS tokens from an authorization server.</span><span class="sxs-lookup"><span data-stu-id="86a49-129">Media Services receives the ACS tokens from an authorization server.</span></span>

<span data-ttu-id="86a49-130">When developing with the Media Services SDK, you can choose to not deal with the tokens because the SDK code managers them for you.</span><span class="sxs-lookup"><span data-stu-id="86a49-130">When developing with the Media Services SDK, you can choose to not deal with the tokens because the SDK code managers them for you.</span></span> <span data-ttu-id="86a49-131">However, letting the SDK fully manage the ACS tokens leads to unnecessary token requests.</span><span class="sxs-lookup"><span data-stu-id="86a49-131">However, letting the SDK fully manage the ACS tokens leads to unnecessary token requests.</span></span> <span data-ttu-id="86a49-132">Requesting tokens takes time and consumes the client and server resources.</span><span class="sxs-lookup"><span data-stu-id="86a49-132">Requesting tokens takes time and consumes the client and server resources.</span></span> <span data-ttu-id="86a49-133">Also, the ACS server throttles the requests if the rate is too high.</span><span class="sxs-lookup"><span data-stu-id="86a49-133">Also, the ACS server throttles the requests if the rate is too high.</span></span> <span data-ttu-id="86a49-134">The limit is 30 requests per second, see [ACS Service Limitations](https://msdn.microsoft.com/library/gg185909.aspx) for more details.</span><span class="sxs-lookup"><span data-stu-id="86a49-134">The limit is 30 requests per second, see [ACS Service Limitations](https://msdn.microsoft.com/library/gg185909.aspx) for more details.</span></span>

<span data-ttu-id="86a49-135">Starting with the Media Services SDK version 3.0.0.0, you can reuse the ACS tokens.</span><span class="sxs-lookup"><span data-stu-id="86a49-135">Starting with the Media Services SDK version 3.0.0.0, you can reuse the ACS tokens.</span></span> <span data-ttu-id="86a49-136">The **CloudMediaContext** constructors that take **MediaServicesCredentials** as a parameter enable sharing the ACS tokens between multiple contexts.</span><span class="sxs-lookup"><span data-stu-id="86a49-136">The **CloudMediaContext** constructors that take **MediaServicesCredentials** as a parameter enable sharing the ACS tokens between multiple contexts.</span></span> <span data-ttu-id="86a49-137">The MediaServicesCredentials class encapsulates the Media Services credentials.</span><span class="sxs-lookup"><span data-stu-id="86a49-137">The MediaServicesCredentials class encapsulates the Media Services credentials.</span></span> <span data-ttu-id="86a49-138">If an ACS token is available and its expiration time is known, you can create a new MediaServicesCredentials instance with the token and pass it to the constructor of CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="86a49-138">If an ACS token is available and its expiration time is known, you can create a new MediaServicesCredentials instance with the token and pass it to the constructor of CloudMediaContext.</span></span> <span data-ttu-id="86a49-139">Note that the Media Services SDK automatically refreshes tokens whenever they expire.</span><span class="sxs-lookup"><span data-stu-id="86a49-139">Note that the Media Services SDK automatically refreshes tokens whenever they expire.</span></span> <span data-ttu-id="86a49-140">There are two ways to reuse ACS tokens, as shown in the examples below.</span><span class="sxs-lookup"><span data-stu-id="86a49-140">There are two ways to reuse ACS tokens, as shown in the examples below.</span></span>

* <span data-ttu-id="86a49-141">You can cache the **MediaServicesCredentials** object in memory (for example, in a static class variable).</span><span class="sxs-lookup"><span data-stu-id="86a49-141">You can cache the **MediaServicesCredentials** object in memory (for example, in a static class variable).</span></span> <span data-ttu-id="86a49-142">Then, pass the cached object to the CloudMediaContext constructor.</span><span class="sxs-lookup"><span data-stu-id="86a49-142">Then, pass the cached object to the CloudMediaContext constructor.</span></span> <span data-ttu-id="86a49-143">The MediaServicesCredentials object contains an ACS token that can be reused if it is still valid.</span><span class="sxs-lookup"><span data-stu-id="86a49-143">The MediaServicesCredentials object contains an ACS token that can be reused if it is still valid.</span></span> <span data-ttu-id="86a49-144">If the token is not valid, it will be refreshed by the Media Services SDK using the credentials given to the MediaServicesCredentials constructor.</span><span class="sxs-lookup"><span data-stu-id="86a49-144">If the token is not valid, it will be refreshed by the Media Services SDK using the credentials given to the MediaServicesCredentials constructor.</span></span>
  
    <span data-ttu-id="86a49-145">Note that the **MediaServicesCredentials** object gets a valid token after the RefreshToken is called.</span><span class="sxs-lookup"><span data-stu-id="86a49-145">Note that the **MediaServicesCredentials** object gets a valid token after the RefreshToken is called.</span></span> <span data-ttu-id="86a49-146">The **CloudMediaContext** calls the **RefreshToken** method in the constructor.</span><span class="sxs-lookup"><span data-stu-id="86a49-146">The **CloudMediaContext** calls the **RefreshToken** method in the constructor.</span></span> <span data-ttu-id="86a49-147">If you are planning to save the token values to an external storage, make sure to check whether the TokenExpiration value is valid before saving the token data.</span><span class="sxs-lookup"><span data-stu-id="86a49-147">If you are planning to save the token values to an external storage, make sure to check whether the TokenExpiration value is valid before saving the token data.</span></span> <span data-ttu-id="86a49-148">If it is not valid, call RefreshToken before caching.</span><span class="sxs-lookup"><span data-stu-id="86a49-148">If it is not valid, call RefreshToken before caching.</span></span>
  
        // Create and cache the Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use the cached credentials to create a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* <span data-ttu-id="86a49-149">You can also cache the AccessToken string and the TokenExpiration values.</span><span class="sxs-lookup"><span data-stu-id="86a49-149">You can also cache the AccessToken string and the TokenExpiration values.</span></span> <span data-ttu-id="86a49-150">The values could later be used to create a new MediaServicesCredentials object with the cached token data.</span><span class="sxs-lookup"><span data-stu-id="86a49-150">The values could later be used to create a new MediaServicesCredentials object with the cached token data.</span></span>  <span data-ttu-id="86a49-151">This is especially useful for scenarios where the token can be securely shared among multiple processes or computers.</span><span class="sxs-lookup"><span data-stu-id="86a49-151">This is especially useful for scenarios where the token can be securely shared among multiple processes or computers.</span></span>
  
    <span data-ttu-id="86a49-152">The following code snippets call the SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage, and UpdateTokenDataInExternalStorageIfNeeded methods that are not defined in this example.</span><span class="sxs-lookup"><span data-stu-id="86a49-152">The following code snippets call the SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage, and UpdateTokenDataInExternalStorageIfNeeded methods that are not defined in this example.</span></span> <span data-ttu-id="86a49-153">You could define these methods to store, retrieve, and update token data in an external storage.</span><span class="sxs-lookup"><span data-stu-id="86a49-153">You could define these methods to store, retrieve, and update token data in an external storage.</span></span> 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from the context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // The SaveTokenDataToExternalStorage method should check 
        // whether the TokenExpiration value is valid before saving the token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    <span data-ttu-id="86a49-154">Use the saved token values to create MediaServicesCredentials.</span><span class="sxs-lookup"><span data-stu-id="86a49-154">Use the saved token values to create MediaServicesCredentials.</span></span>

        var accessToken = "";
        var tokenExpiration = DateTime.UtcNow;

        // Retrieve saved token values.
        GetTokenDataFromExternalStorage(out accessToken, out tokenExpiration);

        // Create a new MediaServicesCredentials object using saved token values.
        MediaServicesCredentials credentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey)
        {
            AccessToken = accessToken,
            TokenExpiration = tokenExpiration
        };

        CloudMediaContext context2 = new CloudMediaContext(credentials);

    <span data-ttu-id="86a49-155">Update the token copy in case the token was updated by the Media Services SDK.</span><span class="sxs-lookup"><span data-stu-id="86a49-155">Update the token copy in case the token was updated by the Media Services SDK.</span></span> 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* <span data-ttu-id="86a49-156">If you have multiple Media Services accounts (for example, for load sharing purposes or Geo-distribution) you can cache MediaServicesCredentials objects using the System.Collections.Concurrent.ConcurrentDictionary collection (the ConcurrentDictionary collection represents a thread-safe collection of key/value pairs that can be accessed by multiple threads concurrently).</span><span class="sxs-lookup"><span data-stu-id="86a49-156">If you have multiple Media Services accounts (for example, for load sharing purposes or Geo-distribution) you can cache MediaServicesCredentials objects using the System.Collections.Concurrent.ConcurrentDictionary collection (the ConcurrentDictionary collection represents a thread-safe collection of key/value pairs that can be accessed by multiple threads concurrently).</span></span> <span data-ttu-id="86a49-157">You can then use the GetOrAdd method to get the cached credentials.</span><span class="sxs-lookup"><span data-stu-id="86a49-157">You can then use the GetOrAdd method to get the cached credentials.</span></span> 
  
        // Declare a static class variable of the ConcurrentDictionary type in which the Media Services credentials will be cached.  
        private static readonly ConcurrentDictionary<string, MediaServicesCredentials> mediaServicesCredentialsCache = 
            new ConcurrentDictionary<string, MediaServicesCredentials>();

        // Cache (or get already cached) Media Services credentials. Use these credentials to create a new CloudMediaContext object.
        static public CloudMediaContext CreateMediaServicesContext(string accountName, string accountKey)
        {
            CloudMediaContext cloudMediaContext;
            MediaServicesCredentials mediaServicesCredentials;

            mediaServicesCredentials = mediaServicesCredentialsCache.GetOrAdd(
                accountName,
                valueFactory => new MediaServicesCredentials(accountName, accountKey));

            cloudMediaContext = new CloudMediaContext(mediaServicesCredentials);

            return cloudMediaContext;
        }

## <a name="connecting-to-a-media-services-account-located-in-the-north-china-region"></a><span data-ttu-id="86a49-158">Connecting to a Media Services account located in the North China region</span><span class="sxs-lookup"><span data-stu-id="86a49-158">Connecting to a Media Services account located in the North China region</span></span>
<span data-ttu-id="86a49-159">If your account is located in the North China region, use the following constructor:</span><span class="sxs-lookup"><span data-stu-id="86a49-159">If your account is located in the North China region, use the following constructor:</span></span>

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

<span data-ttu-id="86a49-160">For example:</span><span class="sxs-lookup"><span data-stu-id="86a49-160">For example:</span></span>

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a><span data-ttu-id="86a49-161">Storing Connection Values in Configuration</span><span class="sxs-lookup"><span data-stu-id="86a49-161">Storing Connection Values in Configuration</span></span>
<span data-ttu-id="86a49-162">It is a highly recommended practice to store connection values, especially sensitive values such as your account name and password, in configuration.</span><span class="sxs-lookup"><span data-stu-id="86a49-162">It is a highly recommended practice to store connection values, especially sensitive values such as your account name and password, in configuration.</span></span> <span data-ttu-id="86a49-163">Also, it is a recommended practice to encrypt sensitive configuration data.</span><span class="sxs-lookup"><span data-stu-id="86a49-163">Also, it is a recommended practice to encrypt sensitive configuration data.</span></span> <span data-ttu-id="86a49-164">You can encrypt the entire configuration file by using the Windows Encrypting File System (EFS).</span><span class="sxs-lookup"><span data-stu-id="86a49-164">You can encrypt the entire configuration file by using the Windows Encrypting File System (EFS).</span></span> <span data-ttu-id="86a49-165">To enable EFS on a file, right-click the file, select **Properties**, and enable encryption in the **Advanced** settings tab. Or you can create a custom solution for encrypting selected portions of a configuration file by using protected configuration.</span><span class="sxs-lookup"><span data-stu-id="86a49-165">To enable EFS on a file, right-click the file, select **Properties**, and enable encryption in the **Advanced** settings tab. Or you can create a custom solution for encrypting selected portions of a configuration file by using protected configuration.</span></span> <span data-ttu-id="86a49-166">See [Encrypting Configuration Information Using Protected Configuration](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span><span class="sxs-lookup"><span data-stu-id="86a49-166">See [Encrypting Configuration Information Using Protected Configuration](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span></span>

<span data-ttu-id="86a49-167">The following App.config file contains the required connection values.</span><span class="sxs-lookup"><span data-stu-id="86a49-167">The following App.config file contains the required connection values.</span></span> <span data-ttu-id="86a49-168">The values in the <appSettings> element are the required values that you got from the Media Services account setup process.</span><span class="sxs-lookup"><span data-stu-id="86a49-168">The values in the <appSettings> element are the required values that you got from the Media Services account setup process.</span></span>

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


<span data-ttu-id="86a49-169">To retrieve connection values from configuration, you can use the **ConfigurationManager** class and then assign the values to fields in your code:</span><span class="sxs-lookup"><span data-stu-id="86a49-169">To retrieve connection values from configuration, you can use the **ConfigurationManager** class and then assign the values to fields in your code:</span></span>

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a><span data-ttu-id="86a49-170">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="86a49-170">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="86a49-171">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="86a49-171">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

