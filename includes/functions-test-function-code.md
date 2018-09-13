## <a name="test"></a><span data-ttu-id="b262a-101">Test the function</span><span class="sxs-lookup"><span data-stu-id="b262a-101">Test the function</span></span>

<span data-ttu-id="b262a-102">Use cURL to test the deployed function on a Mac or Linux computer or using Bash on Windows.</span><span class="sxs-lookup"><span data-stu-id="b262a-102">Use cURL to test the deployed function on a Mac or Linux computer or using Bash on Windows.</span></span> <span data-ttu-id="b262a-103">Execute the following cURL command, replacing the `<app_name>` placeholder with the name of your function app.</span><span class="sxs-lookup"><span data-stu-id="b262a-103">Execute the following cURL command, replacing the `<app_name>` placeholder with the name of your function app.</span></span> <span data-ttu-id="b262a-104">Append the query string `&name=<yourname>` to the URL.</span><span class="sxs-lookup"><span data-stu-id="b262a-104">Append the query string `&name=<yourname>` to the URL.</span></span>

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Function response shown in a browser.](./media/functions-test-function-code/functions-azure-cli-function-test-curl.png)  

<span data-ttu-id="b262a-106">If you don't have cURL available in your command line, enter the same URL in the address of your web browser.</span><span class="sxs-lookup"><span data-stu-id="b262a-106">If you don't have cURL available in your command line, enter the same URL in the address of your web browser.</span></span> <span data-ttu-id="b262a-107">Again, replace the `<app_name>` placeholder with the name of your function app, and append the query string `&name=<yourname>` to the URL and execute the request.</span><span class="sxs-lookup"><span data-stu-id="b262a-107">Again, replace the `<app_name>` placeholder with the name of your function app, and append the query string `&name=<yourname>` to the URL and execute the request.</span></span> 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Function response shown in a browser.](./media/functions-test-function-code/functions-azure-cli-function-test-browser.png)  
