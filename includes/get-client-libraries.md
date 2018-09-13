### <a name="install-via-composer"></a><span data-ttu-id="9433e-101">Install via Composer</span><span class="sxs-lookup"><span data-stu-id="9433e-101">Install via Composer</span></span>
1. <span data-ttu-id="9433e-102">[Install Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="9433e-102">[Install Git][install-git].</span></span> <span data-ttu-id="9433e-103">Note that on Windows, you must also add the Git executable to your PATH environment variable.</span><span class="sxs-lookup"><span data-stu-id="9433e-103">Note that on Windows, you must also add the Git executable to your PATH environment variable.</span></span> 
2. <span data-ttu-id="9433e-104">Create a file named **composer.json** in the root of your project and add the following code to it:</span><span class="sxs-lookup"><span data-stu-id="9433e-104">Create a file named **composer.json** in the root of your project and add the following code to it:</span></span>
   
    ```
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. <span data-ttu-id="9433e-105">Download **[composer.phar][composer-phar]** in your project root.</span><span class="sxs-lookup"><span data-stu-id="9433e-105">Download **[composer.phar][composer-phar]** in your project root.</span></span>
4. <span data-ttu-id="9433e-106">Open a command prompt and execute the following command in your project root</span><span class="sxs-lookup"><span data-stu-id="9433e-106">Open a command prompt and execute the following command in your project root</span></span>
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
