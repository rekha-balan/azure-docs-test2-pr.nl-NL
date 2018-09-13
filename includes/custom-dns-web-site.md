# <a name="configuring-a-custom-domain-name-for-an-azure-website"></a><span data-ttu-id="42055-101">Configuring a custom domain name for an Azure website</span><span class="sxs-lookup"><span data-stu-id="42055-101">Configuring a custom domain name for an Azure website</span></span>
<span data-ttu-id="42055-102">When you create a website, Azure provides a friendly subdomain on the azurewebsites.net domain so your users can access your website using a URL like http://&lt;mysite>.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="42055-102">When you create a website, Azure provides a friendly subdomain on the azurewebsites.net domain so your users can access your website using a URL like http://&lt;mysite>.azurewebsites.net.</span></span> <span data-ttu-id="42055-103">However, if you configure your websites for Shared or Standard mode, you can map your website to your own domain name.</span><span class="sxs-lookup"><span data-stu-id="42055-103">However, if you configure your websites for Shared or Standard mode, you can map your website to your own domain name.</span></span>

<span data-ttu-id="42055-104">Optionally, you can use Azure Traffic Manager to load balance incoming traffic to your website.</span><span class="sxs-lookup"><span data-stu-id="42055-104">Optionally, you can use Azure Traffic Manager to load balance incoming traffic to your website.</span></span> <span data-ttu-id="42055-105">For more information on how Traffic Manager works with Websites, see [Controlling Azure Web Sites Traffic with Azure Traffic Manager][trafficmanager].</span><span class="sxs-lookup"><span data-stu-id="42055-105">For more information on how Traffic Manager works with Websites, see [Controlling Azure Web Sites Traffic with Azure Traffic Manager][trafficmanager].</span></span>

> [!NOTE]
> <span data-ttu-id="42055-106">The procedures in this task apply to Azure Websites; for Cloud Services, see <a href="/develop/net/common-tasks/custom-dns/">Configuring a Custom Domain Name in Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="42055-106">The procedures in this task apply to Azure Websites; for Cloud Services, see <a href="/develop/net/common-tasks/custom-dns/">Configuring a Custom Domain Name in Azure</a>.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="42055-107">The steps in this task require you to configure your websites for Shared or Standard mode, which may change how much you are billed for your subscription.</span><span class="sxs-lookup"><span data-stu-id="42055-107">The steps in this task require you to configure your websites for Shared or Standard mode, which may change how much you are billed for your subscription.</span></span> <span data-ttu-id="42055-108">See <a href="/pricing/details/web-sites/">Websites Pricing Details</a> for more information.</span><span class="sxs-lookup"><span data-stu-id="42055-108">See <a href="/pricing/details/web-sites/">Websites Pricing Details</a> for more information.</span></span>
> 
> 

<span data-ttu-id="42055-109">In this article:</span><span class="sxs-lookup"><span data-stu-id="42055-109">In this article:</span></span>

* [<span data-ttu-id="42055-110">Understanding CNAME and A records</span><span class="sxs-lookup"><span data-stu-id="42055-110">Understanding CNAME and A records</span></span>](#understanding-records)
* [<span data-ttu-id="42055-111">Configure your web sites for shared or standard mode</span><span class="sxs-lookup"><span data-stu-id="42055-111">Configure your web sites for shared or standard mode</span></span>](#bkmk_configsharedmode)
* [<span data-ttu-id="42055-112">Add your web sites to Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="42055-112">Add your web sites to Traffic Manager</span></span>](#trafficmanager)
* [<span data-ttu-id="42055-113">Add a CNAME for your custom domain</span><span class="sxs-lookup"><span data-stu-id="42055-113">Add a CNAME for your custom domain</span></span>](#bkmk_configurecname)
* [<span data-ttu-id="42055-114">Add an A record for your custom domain</span><span class="sxs-lookup"><span data-stu-id="42055-114">Add an A record for your custom domain</span></span>](#bkmk_configurearecord)

<h2><a name="understanding-records"></a><span data-ttu-id="42055-115">Understand CNAME and A records</span><span class="sxs-lookup"><span data-stu-id="42055-115">Understand CNAME and A records</span></span></h2>

<span data-ttu-id="42055-116">CNAME (or alias records) and A records both allow you to associate a domain name with a website, however they each work differently.</span><span class="sxs-lookup"><span data-stu-id="42055-116">CNAME (or alias records) and A records both allow you to associate a domain name with a website, however they each work differently.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="42055-117">CNAME or Alias record</span><span class="sxs-lookup"><span data-stu-id="42055-117">CNAME or Alias record</span></span>
<span data-ttu-id="42055-118">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, to a canonical domain name.</span><span class="sxs-lookup"><span data-stu-id="42055-118">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, to a canonical domain name.</span></span> <span data-ttu-id="42055-119">In this case, the canonical domain name is the either the **&lt;myapp>.azurewebsites.net** domain name of your Azure website or the **&lt;myapp>.trafficmgr.com** domain name of your Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="42055-119">In this case, the canonical domain name is the either the **&lt;myapp>.azurewebsites.net** domain name of your Azure website or the **&lt;myapp>.trafficmgr.com** domain name of your Traffic Manager profile.</span></span> <span data-ttu-id="42055-120">Once created, the CNAME creates an alias for the **&lt;myapp>.azurewebsites.net** or **&lt;myapp>.trafficmgr.com** domain name.</span><span class="sxs-lookup"><span data-stu-id="42055-120">Once created, the CNAME creates an alias for the **&lt;myapp>.azurewebsites.net** or **&lt;myapp>.trafficmgr.com** domain name.</span></span> <span data-ttu-id="42055-121">The CNAME entry will resolve to the IP address of your **&lt;myapp>.azurewebsites.net** or **&lt;myapp>.trafficmgr.com** domain name automatically, so if the IP address of the website changes, you do not have to take any action.</span><span class="sxs-lookup"><span data-stu-id="42055-121">The CNAME entry will resolve to the IP address of your **&lt;myapp>.azurewebsites.net** or **&lt;myapp>.trafficmgr.com** domain name automatically, so if the IP address of the website changes, you do not have to take any action.</span></span>

> [!NOTE]
> <span data-ttu-id="42055-122">Some domain registrars only allow you to map subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com.</span><span class="sxs-lookup"><span data-stu-id="42055-122">Some domain registrars only allow you to map subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com.</span></span> <span data-ttu-id="42055-123">For more information on CNAME records, see the documentation provided by your registrar, <a href="http://en.wikipedia.org/wiki/CNAME_record">the Wikipedia entry on CNAME record</a>, or the <a href="http://tools.ietf.org/html/rfc1035">IETF Domain Names - Implementation and Specification</a> document.</span><span class="sxs-lookup"><span data-stu-id="42055-123">For more information on CNAME records, see the documentation provided by your registrar, <a href="http://en.wikipedia.org/wiki/CNAME_record">the Wikipedia entry on CNAME record</a>, or the <a href="http://tools.ietf.org/html/rfc1035">IETF Domain Names - Implementation and Specification</a> document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="42055-124">A record</span><span class="sxs-lookup"><span data-stu-id="42055-124">A record</span></span>
<span data-ttu-id="42055-125">An A record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, to an IP address.</span><span class="sxs-lookup"><span data-stu-id="42055-125">An A record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, to an IP address.</span></span> <span data-ttu-id="42055-126">In the case of an Azure Website, either the virtual IP of the service or a specific IP address that you purchased for your website.</span><span class="sxs-lookup"><span data-stu-id="42055-126">In the case of an Azure Website, either the virtual IP of the service or a specific IP address that you purchased for your website.</span></span> <span data-ttu-id="42055-127">So the main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span><span class="sxs-lookup"><span data-stu-id="42055-127">So the main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="42055-128">Since an A record is mapped to a static IP address, it cannot automatically resolve changes to the IP address of your website.</span><span class="sxs-lookup"><span data-stu-id="42055-128">Since an A record is mapped to a static IP address, it cannot automatically resolve changes to the IP address of your website.</span></span> <span data-ttu-id="42055-129">An IP address for use with A records is provided when you configure custom domain name settings for your website; however, this value may change if you delete and recreate your website, or change the website mode to back to free.</span><span class="sxs-lookup"><span data-stu-id="42055-129">An IP address for use with A records is provided when you configure custom domain name settings for your website; however, this value may change if you delete and recreate your website, or change the website mode to back to free.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="42055-130">A records cannot be used for load balancing with Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="42055-130">A records cannot be used for load balancing with Traffic Manager.</span></span> <span data-ttu-id="42055-131">For more information, see [Controlling Azure Web Sites Traffic with Azure Traffic Manager][trafficmanager].</span><span class="sxs-lookup"><span data-stu-id="42055-131">For more information, see [Controlling Azure Web Sites Traffic with Azure Traffic Manager][trafficmanager].</span></span>
> 
> 

<a name="bkmk_configsharedmode"></a><h2><span data-ttu-id="42055-132">Configure your websites for shared or standard mode</span><span class="sxs-lookup"><span data-stu-id="42055-132">Configure your websites for shared or standard mode</span></span></h2>

<span data-ttu-id="42055-133">Setting a custom domain name on a website is only available for the Shared and Standard modes for Azure websites.</span><span class="sxs-lookup"><span data-stu-id="42055-133">Setting a custom domain name on a website is only available for the Shared and Standard modes for Azure websites.</span></span> <span data-ttu-id="42055-134">Before switching a website from the Free website mode to the Shared or Standard website mode, you must first remove spending caps in place for your Website subscription.</span><span class="sxs-lookup"><span data-stu-id="42055-134">Before switching a website from the Free website mode to the Shared or Standard website mode, you must first remove spending caps in place for your Website subscription.</span></span> <span data-ttu-id="42055-135">For more information on Shared and Standard mode pricing, see [Pricing Details][PricingDetails].</span><span class="sxs-lookup"><span data-stu-id="42055-135">For more information on Shared and Standard mode pricing, see [Pricing Details][PricingDetails].</span></span>

1. <span data-ttu-id="42055-136">In your browser, open the [Management Portal][portal].</span><span class="sxs-lookup"><span data-stu-id="42055-136">In your browser, open the [Management Portal][portal].</span></span>
2. <span data-ttu-id="42055-137">In the **Websites** tab, click the name of your site.</span><span class="sxs-lookup"><span data-stu-id="42055-137">In the **Websites** tab, click the name of your site.</span></span>
   
    ![][standardmode1]
3. <span data-ttu-id="42055-138">Click the **SCALE** tab.</span><span class="sxs-lookup"><span data-stu-id="42055-138">Click the **SCALE** tab.</span></span>
   
    ![][standardmode2]
4. <span data-ttu-id="42055-139">In the **general** section, set the website mode by clicking **SHARED**.</span><span class="sxs-lookup"><span data-stu-id="42055-139">In the **general** section, set the website mode by clicking **SHARED**.</span></span>
   
    ![][standardmode3]
   
   > [!NOTE]
   > <span data-ttu-id="42055-140">If you will be using Traffic Manager with this website, you must use select Standard mode instead of Shared.</span><span class="sxs-lookup"><span data-stu-id="42055-140">If you will be using Traffic Manager with this website, you must use select Standard mode instead of Shared.</span></span>
   > 
   > 
5. <span data-ttu-id="42055-141">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="42055-141">Click **Save**.</span></span>
6. <span data-ttu-id="42055-142">When prompted about the increase in cost for Shared mode (or for Standard mode if you choose Standard), click **Yes** if you agree.</span><span class="sxs-lookup"><span data-stu-id="42055-142">When prompted about the increase in cost for Shared mode (or for Standard mode if you choose Standard), click **Yes** if you agree.</span></span>
   
    <!--![][standardmode4]-->
   
    <span data-ttu-id="42055-143">**Note**</span><span class="sxs-lookup"><span data-stu-id="42055-143">**Note**</span></span><br />
    <span data-ttu-id="42055-144">If you receive a "Configuring scale for website 'website name' failed" error, you can use the details button to get more information.</span><span class="sxs-lookup"><span data-stu-id="42055-144">If you receive a "Configuring scale for website 'website name' failed" error, you can use the details button to get more information.</span></span>

<a name="trafficmanager"></a><h2><span data-ttu-id="42055-145">(Optional) Add your websites to Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="42055-145">(Optional) Add your websites to Traffic Manager</span></span></h2>

<span data-ttu-id="42055-146">If you want to use your website with Traffic Manager, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="42055-146">If you want to use your website with Traffic Manager, perform the following steps.</span></span>

1. <span data-ttu-id="42055-147">If you do not already have a Traffic Manager profile, use the information in [Create a Traffic Manager profile using Quick Create][createprofile] to create one.</span><span class="sxs-lookup"><span data-stu-id="42055-147">If you do not already have a Traffic Manager profile, use the information in [Create a Traffic Manager profile using Quick Create][createprofile] to create one.</span></span> <span data-ttu-id="42055-148">Note the **.trafficmgr.com** domain name associated with your Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="42055-148">Note the **.trafficmgr.com** domain name associated with your Traffic Manager profile.</span></span> <span data-ttu-id="42055-149">This will be used in a later step.</span><span class="sxs-lookup"><span data-stu-id="42055-149">This will be used in a later step.</span></span>
2. <span data-ttu-id="42055-150">Use the information in [Add or Delete Endpoints][addendpoint] to add your website as an endpoint in your Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="42055-150">Use the information in [Add or Delete Endpoints][addendpoint] to add your website as an endpoint in your Traffic Manager profile.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="42055-151">If your website is not listed when adding an endpoint, verify that it is configured for Standard mode.</span><span class="sxs-lookup"><span data-stu-id="42055-151">If your website is not listed when adding an endpoint, verify that it is configured for Standard mode.</span></span> <span data-ttu-id="42055-152">You must use Standard mode for your website in order to work with Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="42055-152">You must use Standard mode for your website in order to work with Traffic Manager.</span></span>
   > 
   > 
3. <span data-ttu-id="42055-153">Log on to your DNS registrar's website, and go to the page for managing DNS.</span><span class="sxs-lookup"><span data-stu-id="42055-153">Log on to your DNS registrar's website, and go to the page for managing DNS.</span></span> <span data-ttu-id="42055-154">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span><span class="sxs-lookup"><span data-stu-id="42055-154">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
4. <span data-ttu-id="42055-155">Now find where you can select or enter CNAME records.</span><span class="sxs-lookup"><span data-stu-id="42055-155">Now find where you can select or enter CNAME records.</span></span> <span data-ttu-id="42055-156">You may have to select the record type from a drop down, or go to an advanced settings page.</span><span class="sxs-lookup"><span data-stu-id="42055-156">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span> <span data-ttu-id="42055-157">You should look for the words **CNAME**, **Alias**, or **Subdomains**.</span><span class="sxs-lookup"><span data-stu-id="42055-157">You should look for the words **CNAME**, **Alias**, or **Subdomains**.</span></span>
5. <span data-ttu-id="42055-158">You must also provide the domain or subdomain alias for the CNAME.</span><span class="sxs-lookup"><span data-stu-id="42055-158">You must also provide the domain or subdomain alias for the CNAME.</span></span> <span data-ttu-id="42055-159">For example, **www** if you want to create an alias for **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="42055-159">For example, **www** if you want to create an alias for **www.customdomain.com**.</span></span>
6. <span data-ttu-id="42055-160">You must also provide a host name that is the canonical domain name for this CNAME alias.</span><span class="sxs-lookup"><span data-stu-id="42055-160">You must also provide a host name that is the canonical domain name for this CNAME alias.</span></span> <span data-ttu-id="42055-161">This is the **.trafficmgr.com** name for your website.</span><span class="sxs-lookup"><span data-stu-id="42055-161">This is the **.trafficmgr.com** name for your website.</span></span>

<span data-ttu-id="42055-162">For example, the following CNAME record forwards all traffic from **www.contoso.com** to **contoso.trafficmgr.com**, the domain name of a website:</span><span class="sxs-lookup"><span data-stu-id="42055-162">For example, the following CNAME record forwards all traffic from **www.contoso.com** to **contoso.trafficmgr.com**, the domain name of a website:</span></span>

<table border="1" cellspacing="0" cellpadding="5" style="border: 1px solid #000000;">
<tr>
<td><span data-ttu-id="42055-163"><strong>Alias/Host name/Subdomain</strong></span><span class="sxs-lookup"><span data-stu-id="42055-163"><strong>Alias/Host name/Subdomain</strong></span></span></td>
<td><span data-ttu-id="42055-164"><strong>Canonical domain</strong></span><span class="sxs-lookup"><span data-stu-id="42055-164"><strong>Canonical domain</strong></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="42055-165">www</span><span class="sxs-lookup"><span data-stu-id="42055-165">www</span></span></td>
<td><span data-ttu-id="42055-166">contoso.trafficmgr.com</span><span class="sxs-lookup"><span data-stu-id="42055-166">contoso.trafficmgr.com</span></span></td>
</tr>
</table>

<span data-ttu-id="42055-167">A visitor of **www.contoso.com** will never see the true host (contoso.azurewebsite.net), so the forwarding process is invisible to the end user.</span><span class="sxs-lookup"><span data-stu-id="42055-167">A visitor of **www.contoso.com** will never see the true host (contoso.azurewebsite.net), so the forwarding process is invisible to the end user.</span></span>

> [!NOTE]
> <span data-ttu-id="42055-168">If you are using Traffic Manager with a website, you do not need to follow the steps in the following sections, '**Add a CNAME for your custom domain**' and '**Add an A record for your custom domain**'.</span><span class="sxs-lookup"><span data-stu-id="42055-168">If you are using Traffic Manager with a website, you do not need to follow the steps in the following sections, '**Add a CNAME for your custom domain**' and '**Add an A record for your custom domain**'.</span></span> <span data-ttu-id="42055-169">The CNAME record created in the previous steps will route incoming traffic to Traffic Manager, which then routes the traffic to the website endpoint(s).</span><span class="sxs-lookup"><span data-stu-id="42055-169">The CNAME record created in the previous steps will route incoming traffic to Traffic Manager, which then routes the traffic to the website endpoint(s).</span></span>
> 
> 

<a name="bkmk_configurecname"></a><h2><span data-ttu-id="42055-170">Add a CNAME for your custom domain</span><span class="sxs-lookup"><span data-stu-id="42055-170">Add a CNAME for your custom domain</span></span></h2>

<span data-ttu-id="42055-171">To create a CNAME record, you must add a new entry in the DNS table for your custom domain by using tools provided by your registrar.</span><span class="sxs-lookup"><span data-stu-id="42055-171">To create a CNAME record, you must add a new entry in the DNS table for your custom domain by using tools provided by your registrar.</span></span> <span data-ttu-id="42055-172">Each registrar has a similar but slightly different method of specifying a CNAME record, but the concepts are the same.</span><span class="sxs-lookup"><span data-stu-id="42055-172">Each registrar has a similar but slightly different method of specifying a CNAME record, but the concepts are the same.</span></span>

1. <span data-ttu-id="42055-173">Use one of these methods to find the **.azurewebsite.net** domain name assigned to your website.</span><span class="sxs-lookup"><span data-stu-id="42055-173">Use one of these methods to find the **.azurewebsite.net** domain name assigned to your website.</span></span>
   
   * <span data-ttu-id="42055-174">Login to the [Azure Management Portal][portal], select your website, select **Dashboard**, and then find the **Site URL** entry in the **quick glance** section.</span><span class="sxs-lookup"><span data-stu-id="42055-174">Login to the [Azure Management Portal][portal], select your website, select **Dashboard**, and then find the **Site URL** entry in the **quick glance** section.</span></span>
   * <span data-ttu-id="42055-175">Install and configure [Azure Powershell](/manage/install-and-configure-windows-powershell/), and then use the following command:</span><span class="sxs-lookup"><span data-stu-id="42055-175">Install and configure [Azure Powershell](/manage/install-and-configure-windows-powershell/), and then use the following command:</span></span>
     
           get-azurewebsite yoursitename | select hostnames
   * <span data-ttu-id="42055-176">Install and configure the [Azure Command Line Interface](/manage/install-and-configure-cli/), and then use the following command:</span><span class="sxs-lookup"><span data-stu-id="42055-176">Install and configure the [Azure Command Line Interface](/manage/install-and-configure-cli/), and then use the following command:</span></span>
     
           azure site domain list yoursitename
     
     <span data-ttu-id="42055-177">Save this **.azurewebsite.net** name, as it will be used in the following steps.</span><span class="sxs-lookup"><span data-stu-id="42055-177">Save this **.azurewebsite.net** name, as it will be used in the following steps.</span></span>
2. <span data-ttu-id="42055-178">Log on to your DNS registrar's website, and go to the page for managing DNS.</span><span class="sxs-lookup"><span data-stu-id="42055-178">Log on to your DNS registrar's website, and go to the page for managing DNS.</span></span> <span data-ttu-id="42055-179">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span><span class="sxs-lookup"><span data-stu-id="42055-179">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="42055-180">Now find where you can select or enter CNAME records.</span><span class="sxs-lookup"><span data-stu-id="42055-180">Now find where you can select or enter CNAME records.</span></span> <span data-ttu-id="42055-181">You may have to select the record type from a drop down, or go to an advanced settings page.</span><span class="sxs-lookup"><span data-stu-id="42055-181">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span> <span data-ttu-id="42055-182">You should look for the words **CNAME**, **Alias**, or **Subdomains**.</span><span class="sxs-lookup"><span data-stu-id="42055-182">You should look for the words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="42055-183">You must also provide the domain or subdomain alias for the CNAME.</span><span class="sxs-lookup"><span data-stu-id="42055-183">You must also provide the domain or subdomain alias for the CNAME.</span></span> <span data-ttu-id="42055-184">For example, **www** if you want to create an alias for **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="42055-184">For example, **www** if you want to create an alias for **www.customdomain.com**.</span></span> <span data-ttu-id="42055-185">If you want to create an alias for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span><span class="sxs-lookup"><span data-stu-id="42055-185">If you want to create an alias for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="42055-186">You must also provide a host name that is the canonical domain name for this CNAME alias.</span><span class="sxs-lookup"><span data-stu-id="42055-186">You must also provide a host name that is the canonical domain name for this CNAME alias.</span></span> <span data-ttu-id="42055-187">This is the **.azurewebsite.net** name for your website.</span><span class="sxs-lookup"><span data-stu-id="42055-187">This is the **.azurewebsite.net** name for your website.</span></span>

<span data-ttu-id="42055-188">For example, the following CNAME record forwards all traffic from **www.contoso.com** to **contoso.azurewebsite.net**, the domain name of a website:</span><span class="sxs-lookup"><span data-stu-id="42055-188">For example, the following CNAME record forwards all traffic from **www.contoso.com** to **contoso.azurewebsite.net**, the domain name of a website:</span></span>

<table border="1" cellspacing="0" cellpadding="5" style="border: 1px solid #000000;">
<tr>
<td><span data-ttu-id="42055-189"><strong>Alias/Host name/Subdomain</strong></span><span class="sxs-lookup"><span data-stu-id="42055-189"><strong>Alias/Host name/Subdomain</strong></span></span></td>
<td><span data-ttu-id="42055-190"><strong>Canonical domain</strong></span><span class="sxs-lookup"><span data-stu-id="42055-190"><strong>Canonical domain</strong></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="42055-191">www</span><span class="sxs-lookup"><span data-stu-id="42055-191">www</span></span></td>
<td><span data-ttu-id="42055-192">contoso.azurewebsite.net</span><span class="sxs-lookup"><span data-stu-id="42055-192">contoso.azurewebsite.net</span></span></td>
</tr>
</table>

<span data-ttu-id="42055-193">A visitor of **www.contoso.com** will never see the true host (contoso.azurewebsite.net), so the forwarding process is invisible to the end user.</span><span class="sxs-lookup"><span data-stu-id="42055-193">A visitor of **www.contoso.com** will never see the true host (contoso.azurewebsite.net), so the forwarding process is invisible to the end user.</span></span>

> [!NOTE]
> <span data-ttu-id="42055-194">The example above only applies to traffic at the **www** subdomain.</span><span class="sxs-lookup"><span data-stu-id="42055-194">The example above only applies to traffic at the **www** subdomain.</span></span> <span data-ttu-id="42055-195">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span><span class="sxs-lookup"><span data-stu-id="42055-195">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="42055-196">If you want to direct  traffic from subdomains, such as \*.contoso.com, to your azurewebsite.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span><span class="sxs-lookup"><span data-stu-id="42055-196">If you want to direct  traffic from subdomains, such as \*.contoso.com, to your azurewebsite.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="42055-197">It can take some time for your CNAME to propagate through the DNS system.</span><span class="sxs-lookup"><span data-stu-id="42055-197">It can take some time for your CNAME to propagate through the DNS system.</span></span> <span data-ttu-id="42055-198">You cannot set the CNAME for the website until the CNAME has propagated.</span><span class="sxs-lookup"><span data-stu-id="42055-198">You cannot set the CNAME for the website until the CNAME has propagated.</span></span> <span data-ttu-id="42055-199">You can use a service such as <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> to verify that the CNAME is available.</span><span class="sxs-lookup"><span data-stu-id="42055-199">You can use a service such as <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> to verify that the CNAME is available.</span></span>
> 
> 

### <a name="add-the-domain-name-to-your-website"></a><span data-ttu-id="42055-200">Add the domain name to your website</span><span class="sxs-lookup"><span data-stu-id="42055-200">Add the domain name to your website</span></span>
<span data-ttu-id="42055-201">After the CNAME record for domain name has propagated, you must associate it with your website.</span><span class="sxs-lookup"><span data-stu-id="42055-201">After the CNAME record for domain name has propagated, you must associate it with your website.</span></span> <span data-ttu-id="42055-202">You can add the custom domain name defined by the CNAME record to your website by using either the Azure Command-Line Interface (Azure CLI) or by using the Azure Management Portal.</span><span class="sxs-lookup"><span data-stu-id="42055-202">You can add the custom domain name defined by the CNAME record to your website by using either the Azure Command-Line Interface (Azure CLI) or by using the Azure Management Portal.</span></span>

<span data-ttu-id="42055-203">**To add a domain name using the command-line tools**</span><span class="sxs-lookup"><span data-stu-id="42055-203">**To add a domain name using the command-line tools**</span></span>

<span data-ttu-id="42055-204">Install and configure the [Azure Command-Line Interface](/manage/install-and-configure-cli/), and then use the following command:</span><span class="sxs-lookup"><span data-stu-id="42055-204">Install and configure the [Azure Command-Line Interface](/manage/install-and-configure-cli/), and then use the following command:</span></span>

    azure site domain add customdomain yoursitename

<span data-ttu-id="42055-205">For example, the following will add a custom domain name of **www.contoso.com** to the **contoso.azurewebsite.net** website:</span><span class="sxs-lookup"><span data-stu-id="42055-205">For example, the following will add a custom domain name of **www.contoso.com** to the **contoso.azurewebsite.net** website:</span></span>

    azure site domain add www.contoso.com contoso

<span data-ttu-id="42055-206">You can confirm that the custom domain name was added to the website by using the following command:</span><span class="sxs-lookup"><span data-stu-id="42055-206">You can confirm that the custom domain name was added to the website by using the following command:</span></span>

    azure site domain list yoursitename

<span data-ttu-id="42055-207">The list returned by this command should contain the custom domain name, as well as the default **.azurewebsite.net** entry.</span><span class="sxs-lookup"><span data-stu-id="42055-207">The list returned by this command should contain the custom domain name, as well as the default **.azurewebsite.net** entry.</span></span>

<span data-ttu-id="42055-208">**To add a domain name using the Azure Management Portal**</span><span class="sxs-lookup"><span data-stu-id="42055-208">**To add a domain name using the Azure Management Portal**</span></span>

1. <span data-ttu-id="42055-209">In your browser, open the [Azure Management Portal][portal].</span><span class="sxs-lookup"><span data-stu-id="42055-209">In your browser, open the [Azure Management Portal][portal].</span></span>
2. <span data-ttu-id="42055-210">In the **Websites** tab, click the name of your site, select **Dashboard**, and then select **Manage Domains** from the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="42055-210">In the **Websites** tab, click the name of your site, select **Dashboard**, and then select **Manage Domains** from the bottom of the page.</span></span>
   
    ![][setcname2]
3. <span data-ttu-id="42055-211">In the **DOMAIN NAMES** text box, type the domain name that you have configured.</span><span class="sxs-lookup"><span data-stu-id="42055-211">In the **DOMAIN NAMES** text box, type the domain name that you have configured.</span></span>
   
    ![][setcname3]
4. <span data-ttu-id="42055-212">Click the check mark to accept the domain name.</span><span class="sxs-lookup"><span data-stu-id="42055-212">Click the check mark to accept the domain name.</span></span>

<span data-ttu-id="42055-213">Once configuration has completed, the custom domain name will be listed in the **domain names** section of the **Configure** page of your website.</span><span class="sxs-lookup"><span data-stu-id="42055-213">Once configuration has completed, the custom domain name will be listed in the **domain names** section of the **Configure** page of your website.</span></span>

<a name="bkmk_configurearecord"></a><h2><span data-ttu-id="42055-214">Add an A Record for your custom domain</span><span class="sxs-lookup"><span data-stu-id="42055-214">Add an A Record for your custom domain</span></span></h2>

<span data-ttu-id="42055-215">To create an A record, you must first find the IP address of your website.</span><span class="sxs-lookup"><span data-stu-id="42055-215">To create an A record, you must first find the IP address of your website.</span></span> <span data-ttu-id="42055-216">Then add an entry in the DNS table for your custom domain by using the tools provided by your registrar.</span><span class="sxs-lookup"><span data-stu-id="42055-216">Then add an entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="42055-217">Each registrar has a similar but slightly different method of specifying an A record, but the concepts are the same.</span><span class="sxs-lookup"><span data-stu-id="42055-217">Each registrar has a similar but slightly different method of specifying an A record, but the concepts are the same.</span></span> <span data-ttu-id="42055-218">In addition to creating an A record, you must also create a CNAME record that Azure uses to verify the A record.</span><span class="sxs-lookup"><span data-stu-id="42055-218">In addition to creating an A record, you must also create a CNAME record that Azure uses to verify the A record.</span></span>

1. <span data-ttu-id="42055-219">In your browser, open the [Azure Management Portal][portal].</span><span class="sxs-lookup"><span data-stu-id="42055-219">In your browser, open the [Azure Management Portal][portal].</span></span>
2. <span data-ttu-id="42055-220">In the **Websites** tab, click the name of your site, select **Dashboard**, and then select **Manage Domains** from the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="42055-220">In the **Websites** tab, click the name of your site, select **Dashboard**, and then select **Manage Domains** from the bottom of the screen.</span></span>
   
    ![][setcname2]
3. <span data-ttu-id="42055-221">On the **Manage custom domains** dialog, locate **The IP Address to use when configuring A records**.</span><span class="sxs-lookup"><span data-stu-id="42055-221">On the **Manage custom domains** dialog, locate **The IP Address to use when configuring A records**.</span></span> <span data-ttu-id="42055-222">Copy the IP address.</span><span class="sxs-lookup"><span data-stu-id="42055-222">Copy the IP address.</span></span> <span data-ttu-id="42055-223">This will be used when creating the A record.</span><span class="sxs-lookup"><span data-stu-id="42055-223">This will be used when creating the A record.</span></span>
4. <span data-ttu-id="42055-224">On the **Manage custom domains** dialog, note awverify domain name at the end of the text at the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="42055-224">On the **Manage custom domains** dialog, note awverify domain name at the end of the text at the top of the dialog.</span></span> <span data-ttu-id="42055-225">It should be **awverify.mysite.azurewebsites.net** where **mysite** is the name of your website.</span><span class="sxs-lookup"><span data-stu-id="42055-225">It should be **awverify.mysite.azurewebsites.net** where **mysite** is the name of your website.</span></span> <span data-ttu-id="42055-226">Copy this, as it is the domain name used when creating the verification CNAME record.</span><span class="sxs-lookup"><span data-stu-id="42055-226">Copy this, as it is the domain name used when creating the verification CNAME record.</span></span>
5. <span data-ttu-id="42055-227">Log on to your DNS registrar's website, and go to the page for managing DNS.</span><span class="sxs-lookup"><span data-stu-id="42055-227">Log on to your DNS registrar's website, and go to the page for managing DNS.</span></span> <span data-ttu-id="42055-228">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span><span class="sxs-lookup"><span data-stu-id="42055-228">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
6. <span data-ttu-id="42055-229">Find where you can select or enter A and CNAME records.</span><span class="sxs-lookup"><span data-stu-id="42055-229">Find where you can select or enter A and CNAME records.</span></span> <span data-ttu-id="42055-230">You may have to select the record type from a drop down, or go to an advanced settings page.</span><span class="sxs-lookup"><span data-stu-id="42055-230">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span>
7. <span data-ttu-id="42055-231">Perform the following steps to create the A record:</span><span class="sxs-lookup"><span data-stu-id="42055-231">Perform the following steps to create the A record:</span></span>
   
   1. <span data-ttu-id="42055-232">Select or enter the domain or subdomain that will use the A record.</span><span class="sxs-lookup"><span data-stu-id="42055-232">Select or enter the domain or subdomain that will use the A record.</span></span> <span data-ttu-id="42055-233">For example, select **www** if you want to create an alias for **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="42055-233">For example, select **www** if you want to create an alias for **www.customdomain.com**.</span></span> <span data-ttu-id="42055-234">If you want to create a wildcard entry for all subdomains, enter '\*\*\*\*\*'.</span><span class="sxs-lookup"><span data-stu-id="42055-234">If you want to create a wildcard entry for all subdomains, enter '\*\*\*\*\*'.</span></span> <span data-ttu-id="42055-235">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="42055-235">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
      
       <span data-ttu-id="42055-236">If you want to create an A record for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span><span class="sxs-lookup"><span data-stu-id="42055-236">If you want to create an A record for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
   2. <span data-ttu-id="42055-237">Enter the IP address of your cloud service in the provided field.</span><span class="sxs-lookup"><span data-stu-id="42055-237">Enter the IP address of your cloud service in the provided field.</span></span> <span data-ttu-id="42055-238">This associates the domain entry used in the A record with the IP address of your cloud service deployment.</span><span class="sxs-lookup"><span data-stu-id="42055-238">This associates the domain entry used in the A record with the IP address of your cloud service deployment.</span></span>
      
       <span data-ttu-id="42055-239">For example, the following A record forwards all traffic from **contoso.com** to **137.135.70.239**, the IP address of our deployed application:</span><span class="sxs-lookup"><span data-stu-id="42055-239">For example, the following A record forwards all traffic from **contoso.com** to **137.135.70.239**, the IP address of our deployed application:</span></span>
      
       <table border="1" cellspacing="0" cellpadding="5" style="border: 1px solid #000000;">
       <tr>
       <td><span data-ttu-id="42055-240"><strong>Host name/Subdomain</strong></span><span class="sxs-lookup"><span data-stu-id="42055-240"><strong>Host name/Subdomain</strong></span></span></td>
       <td><span data-ttu-id="42055-241"><strong>IP address</strong></span><span class="sxs-lookup"><span data-stu-id="42055-241"><strong>IP address</strong></span></span></td>
       </tr>
       <tr>
       <td>@</td>
       <td><span data-ttu-id="42055-242">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="42055-242">137.135.70.239</span></span></td>
       </tr>
       </table>
      
       <span data-ttu-id="42055-243">This example demonstrates creating an A record for the root domain.</span><span class="sxs-lookup"><span data-stu-id="42055-243">This example demonstrates creating an A record for the root domain.</span></span> <span data-ttu-id="42055-244">If you wish to create a wildcard entry to cover all subdomains, you would enter '\*\*\*\*\*' as the subdomain.</span><span class="sxs-lookup"><span data-stu-id="42055-244">If you wish to create a wildcard entry to cover all subdomains, you would enter '\*\*\*\*\*' as the subdomain.</span></span>
8. <span data-ttu-id="42055-245">Next, create a CNAME record that has an alias of **awverify**, and a canonical domain of **awverify.mysite.azurewebsites.net** that you obtained earlier.</span><span class="sxs-lookup"><span data-stu-id="42055-245">Next, create a CNAME record that has an alias of **awverify**, and a canonical domain of **awverify.mysite.azurewebsites.net** that you obtained earlier.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="42055-246">While an alias of awverify may work for some registrars, others may require the full alias domain name of awverify.www.customdomainname.com or awverify.customdomainname.com.</span><span class="sxs-lookup"><span data-stu-id="42055-246">While an alias of awverify may work for some registrars, others may require the full alias domain name of awverify.www.customdomainname.com or awverify.customdomainname.com.</span></span>
   > 
   > 
   
    <span data-ttu-id="42055-247">For example, the following will create an CNAME record that Azure can use to verify the A record configuration.</span><span class="sxs-lookup"><span data-stu-id="42055-247">For example, the following will create an CNAME record that Azure can use to verify the A record configuration.</span></span>
   
    <table border="1" cellspacing="0" cellpadding="5" style="border: 1px solid #000000;">
    <tr>
    <td><span data-ttu-id="42055-248"><strong>Alias/Host name/Subdomain</strong></span><span class="sxs-lookup"><span data-stu-id="42055-248"><strong>Alias/Host name/Subdomain</strong></span></span></td>
    <td><span data-ttu-id="42055-249"><strong>Canonical domain</strong></span><span class="sxs-lookup"><span data-stu-id="42055-249"><strong>Canonical domain</strong></span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="42055-250">awverify</span><span class="sxs-lookup"><span data-stu-id="42055-250">awverify</span></span></td>
    <td><span data-ttu-id="42055-251">awverify.contoso.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="42055-251">awverify.contoso.azurewebsites.net</span></span></td>
    </tr>
    </table>

> [!NOTE]
> <span data-ttu-id="42055-252">It can take some time for the awverify CNAME to propagate through the DNS system.</span><span class="sxs-lookup"><span data-stu-id="42055-252">It can take some time for the awverify CNAME to propagate through the DNS system.</span></span> <span data-ttu-id="42055-253">You cannot set the custom domain name defined by the A record for the website until the awverify CNAME has propagated.</span><span class="sxs-lookup"><span data-stu-id="42055-253">You cannot set the custom domain name defined by the A record for the website until the awverify CNAME has propagated.</span></span> <span data-ttu-id="42055-254">You can use a service such as <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> to verify that the CNAME is available.</span><span class="sxs-lookup"><span data-stu-id="42055-254">You can use a service such as <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> to verify that the CNAME is available.</span></span>
> 
> 

### <a name="add-the-domain-name-to-your-website"></a><span data-ttu-id="42055-255">Add the domain name to your website</span><span class="sxs-lookup"><span data-stu-id="42055-255">Add the domain name to your website</span></span>
<span data-ttu-id="42055-256">After the **awverify** CNAME record for domain name has propagated, you can then associate the custom domain defined by the A record with your website.</span><span class="sxs-lookup"><span data-stu-id="42055-256">After the **awverify** CNAME record for domain name has propagated, you can then associate the custom domain defined by the A record with your website.</span></span> <span data-ttu-id="42055-257">You can add the custom domain name defined by the A record to your website by using either the Azure CLI or by using the Azure Management Portal.</span><span class="sxs-lookup"><span data-stu-id="42055-257">You can add the custom domain name defined by the A record to your website by using either the Azure CLI or by using the Azure Management Portal.</span></span>

<span data-ttu-id="42055-258">**To add a domain name using the Azure Command-Line Interface (Azure CLI)**</span><span class="sxs-lookup"><span data-stu-id="42055-258">**To add a domain name using the Azure Command-Line Interface (Azure CLI)**</span></span>

<span data-ttu-id="42055-259">Install and configure the [Azure CLI](/manage/install-and-configure-cli/), and then use the following command:</span><span class="sxs-lookup"><span data-stu-id="42055-259">Install and configure the [Azure CLI](/manage/install-and-configure-cli/), and then use the following command:</span></span>

    azure site domain add customdomain yoursitename

<span data-ttu-id="42055-260">For example, the following will add a custom domain name of **contoso.com** to the **contoso.azurewebsite.net** website:</span><span class="sxs-lookup"><span data-stu-id="42055-260">For example, the following will add a custom domain name of **contoso.com** to the **contoso.azurewebsite.net** website:</span></span>

    azure site domain add contoso.com contoso

<span data-ttu-id="42055-261">You can confirm that the custom domain name was added to the website by using the following command:</span><span class="sxs-lookup"><span data-stu-id="42055-261">You can confirm that the custom domain name was added to the website by using the following command:</span></span>

    azure site domain list yoursitename

<span data-ttu-id="42055-262">The list returned by this command should contain the custom domain name, as well as the default **.azurewebsite.net** entry.</span><span class="sxs-lookup"><span data-stu-id="42055-262">The list returned by this command should contain the custom domain name, as well as the default **.azurewebsite.net** entry.</span></span>

<span data-ttu-id="42055-263">**To add a domain name using the Azure Management Portal**</span><span class="sxs-lookup"><span data-stu-id="42055-263">**To add a domain name using the Azure Management Portal**</span></span>

1. <span data-ttu-id="42055-264">In your browser, open the [Azure Management Portal][portal].</span><span class="sxs-lookup"><span data-stu-id="42055-264">In your browser, open the [Azure Management Portal][portal].</span></span>
2. <span data-ttu-id="42055-265">In the **Websites** tab, click the name of your site, select **Dashboard**, and then select **Manage Domains** from the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="42055-265">In the **Websites** tab, click the name of your site, select **Dashboard**, and then select **Manage Domains** from the bottom of the page.</span></span>
   
    ![][setcname2]
3. <span data-ttu-id="42055-266">In the **DOMAIN NAMES** text box, type the domain name that you have configured.</span><span class="sxs-lookup"><span data-stu-id="42055-266">In the **DOMAIN NAMES** text box, type the domain name that you have configured.</span></span>
   
    ![][setcname3]
4. <span data-ttu-id="42055-267">Click the check mark to accept the domain name.</span><span class="sxs-lookup"><span data-stu-id="42055-267">Click the check mark to accept the domain name.</span></span>

<span data-ttu-id="42055-268">Once configuration has completed, the custom domain name will be listed in the **domain names** section of the **Configure** page of your website.</span><span class="sxs-lookup"><span data-stu-id="42055-268">Once configuration has completed, the custom domain name will be listed in the **domain names** section of the **Configure** page of your website.</span></span>

> [!NOTE]
> <span data-ttu-id="42055-269">After you have added the custom domain name defined by the A record to your website, you can remove the awverify CNAME record using the tools provided by your registrar.</span><span class="sxs-lookup"><span data-stu-id="42055-269">After you have added the custom domain name defined by the A record to your website, you can remove the awverify CNAME record using the tools provided by your registrar.</span></span> <span data-ttu-id="42055-270">However, if you wish to add another A record in the future, you will have to recreate the awverify record before you can associate the new domain name defined by the new A record with the website.</span><span class="sxs-lookup"><span data-stu-id="42055-270">However, if you wish to add another A record in the future, you will have to recreate the awverify record before you can associate the new domain name defined by the new A record with the website.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="42055-271">Next steps</span><span class="sxs-lookup"><span data-stu-id="42055-271">Next steps</span></span>
* [<span data-ttu-id="42055-272">How to manage web sites</span><span class="sxs-lookup"><span data-stu-id="42055-272">How to manage web sites</span></span>](/manage/services/web-sites/how-to-manage-websites/)
* [<span data-ttu-id="42055-273">Configure an SSL certificate for Web Sites</span><span class="sxs-lookup"><span data-stu-id="42055-273">Configure an SSL certificate for Web Sites</span></span>](/develop/net/common-tasks/enable-ssl-web-site/)

<!-- Bookmarks -->

[Configure your web sites for shared mode]: #bkmk_configsharedmode
[Configure the CNAME on your domain registrar]: #bkmk_configurecname
[Configure a CNAME verification record on your domain registrar]: #bkmk_configurecname
[Configure an A record for the domain name]:#bkmk_configurearecord
[Set the domain name in management portal]: #bkmk_setcname

<!-- Links -->

[PricingDetails]: /pricing/details/
[portal]: http://manage.windowsazure.com
[digweb]: http://www.digwebinterface.com/
[cloudservicedns]: ../articles/custom-dns.md
[trafficmanager]: ../articles/app-service-web/web-sites-traffic-manager.md
[addendpoint]: ../articles/traffic-manager/traffic-manager-endpoints.md
[createprofile]: ../articles/traffic-manager/traffic-manager-manage-profiles.md

<!-- images -->

[setcname1]: ../media/dncmntask-cname-5.png


<!-- images -->
[standardmode1]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/custom-dns-web-site/dncmntask-cname-1.png
[standardmode2]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/custom-dns-web-site/dncmntask-cname-2.png
[standardmode3]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/custom-dns-web-site/dncmntask-cname-3.png
[standardmode4]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/custom-dns-web-site/dncmntask-cname-4.png


[setcname2]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/custom-dns-web-site/dncmntask-cname-6.png
[setcname3]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/custom-dns-web-site/dncmntask-cname-7.png






