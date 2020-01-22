*****************************************************************
*        uSkinned Fabric Starter Kit Installation Guide         *
*****************************************************************

Umbraco Version 8
*****************************************************************

* The Fabric Starter Kit must be installed on a clean version of Umbraco V8 with no other starter kits or websites previously installed or configured.

* Refer to our guides for further help on setting up your Starter Kit. https://uskinned.net/guides/

* For further guidance on the HTML framework used with this theme go to: http://getbootstrap.com/


IMPORTANT
*****************************************************************
Only install this package against versions we have tested.

We have confirmed that this package works against:

8.3 - 8.4


*****************************************************************
*                   POST INSTALLATION STEPS                     *                    
*****************************************************************
Following successful installation of your uSkinned Starter Kit you will receive a website with demo pages to get you started.

Obviously you will want to start editing the content, adding, editing and deleting pages so that the website works for your individual needs.

As well as sorting out your website content there are a few more tasks that you should complete before your website is ready to go live to the public.


uSkinned Section
****************************************************************
After installation is complete go to Users (Section) > Groups (Icon) > Administrators.

Add uSkinned to Assigned sections.

Logout and log back in again to see uSkinned Section.


Package Licence
****************************************************************
Your uSkinned Theme will work unrestricted on localhost however you will need to add your license file to the /bin folder for live domains. Your license file can be configured and downloaded from your members area. 

The status of your license can be viewed via the 'uSKinned' section of Umbraco. From this section you can see if your license file has been installed. You can either upload your license file via this section or manually add your license file to the /bin directory of your website.

Please note, if your website is accessed from a domain that is not listed in your license file it will immediately invalidate your license. An invalid license message will remain until you restart your website. Your website must only be accessed from a valid domain.

If you have more than one domain pointing to your website, please refer to the following blog post on setting up domain redirects correctly:

https://uskinned.net/blog/posts/2017/june/quick-tip-assign-multiple-hostnames-to-the-one-production-domain-correctly/


Blog
****************************************************************
This theme comes with a Blog section preinstalled. Blog commenting is controlled via DISQUS (https://disqus.com/). To enable commenting on your website you will need to signup for a free account with DISQUS and create a username which is unique to your website.

You will then need to paste this username into the Umbraco CMS. Navigate to the following node in the Content Section of the Umbraco CMS:

Website Configuration > Global Settings

On the 'General Settings' tab paste your DISQUS username into the 'Disqus username' field.


Contact Form
****************************************************************
This theme comes with a Contact page and associated Contact form preinstalled. To enable your contact form to send its completed field information to a specific email address you will need to complete the following steps.

First of all you will need to specify the email address that contact form submissions should be sent to. Navigate to the following node in the Content Section of the Umbraco CMS:

Home > Contact > Components > Contact Form

On the 'Contact Form' tab update the field 'Recipient Email address' with the correct recipient email address for your website.

When the Contact Form is submitted it will send an email to the email address entered in the above step containing the information that was entered into the form fields. Your website needs valid SMTP details to send this email.

A common approach is to use a third party SMTP provider. If you wish, you can sign up for a free account with SendGrid (https://sendgrid.com). The free package will allow you to send 100 emails/day from your account per month which should be more than enough for most websites.

You will then need to update the web.config file located at the root level of your websites file system with your SMTP details. Look for the following and update values marked with ***** with your own SMTP details:

<system.net>
   <mailSettings>
      <smtp from="*****">
         <network host="*****" userName="*****" password="*****" />
      </smtp>
   </mailSettings>
</system.net>


Newsletter Signup
****************************************************************
This theme comes with a number of places where a website visitor can signup to your Newsletter. Newsletter signups are recorded using one of two email marketing platforms, Campaign Monitor (https://www.campaignmonitor.com/) or MailChimp (http://mailchimp.com/). These email marketing platforms are completely free to use to store your Newsletter subscriptions. You can export your subscriber lists for free also. You are only charged if you want to send emails to your subscriber lists from these platforms.

To enable Newsletter signup on your website you will need to signup for a new account with either Campaign Monitor or MailChimp. You will then need to create a subscriber list within your chosen platform. Each platform will give you a unique API key for your account and a unique Subscriber List ID for the subscriber list you have created.

Once you have this information, navigate to the following node in the Content Section of the Umbraco CMS:

Website Configuration > Global Settings

On the 'Default Newsletter Settings' tab select your chosen email marketing platform and paste your API Key and Subscriber List ID into the related fields.


Custom Error Page
****************************************************************
During the setup of your website you want to be able to see any errors that may occur when you make changes to the code. When your website goes live to the public it is better to show a friendly error message to your website visitors. With your theme we have provided a static HTML page that can be used to show a friendly error page. 

You will need to update the web.config file located at the root level of your websites file system with the location of your friendly error page. Look for the customErrors section and update as follows: 

<customErrors mode="On" defaultRedirect="~/error.html" />


Robots File
****************************************************************
If you are using the Robots TXT node to control your robots.txt file you will need to add the following rewrite rule to your web.config file

<rewrite>
  <rules>
    <rule name="Robots TXT" stopProcessing="true">
      <match url="robots.txt" />
      <action type="Rewrite" url="robots-txt" />
    </rule>
  </rules>
</rewrite>

IIS URL Rewrite module must be installed on your webserver to use this feature.


Password Protected Members Area
****************************************************************
This theme comes with a Password Protected Members Area which you can use to provide content to website visitors who have a valid member account for accessing content created within this section of your website.

During installation of your theme a Member Group is created called 'Main Client'.

To allow access to the Password Protected Members Area you must create a new Member within the Members area of the Umbraco CMS.

On the 'Properties' tab of your member you must add the 'Main Client' to the Member Group for this Member.

Once you have created this member you will be able to login to the Password Protected Members Area using your members account details.


Allowed Content Types
****************************************************************
When you start playing about with the content of your theme you will notice that some of the Document Types that are present when you install your theme cannot be created. An example of this is your Blog Landing Page. You will see that there is a Blog node present below the Homepage of your website however you cannot create a new Blog node. The reason we do this is to keep your website CMS simple to Content Editors. Once a Blog is created, chances are that you will never create another one. If for some reason you want to create more than one Blog on your website or you delete the existing Blog node and want to recreate it you will need to allow this Document Type to be created below the Homepage Document Type.

To do this navigate to the Settings Section of the Umbraco CMS. Expand the 'Document Types' folder and go to Web Pages > Homepage.

Update the 'Allowed Child Node Types' so that the Blog Landing Page is included.

The same applies for any other Document Types that you want to allow to be created below a particular Document Type.


Visual Studio Web Application
****************************************************************
If you setup your Umbraco website as a Visual Studio Web Application you will need to let your Visual Studio Project know about any new files that are added after installing your uSkinned 
Package. If you dont do this any deployment from Visual Studio will not include all of the necessary files required for your website to run properly.

The following files and folders should be included with your project:

/App_Code (All files)
/App_Plugins/ (All files)  
/bin/createsend-dotnet.dll
/bin/dotless.AspNet.dll
/bin/dotless.Core.dll
/bin/MailChimp.dll
/bin/ServiceStack.Text.dll
/bin/USNStarterKit.dll
/bin/PackageGarden.Licensing.dll
/bin/uskinned-v8-theme.lic
/bin/Umbraco.Web.PublishedModels.dll
/bin/Microsoft.Extensions.DependencyInjection.dll
/css (All files)
/images (All files)
/less (All files)
/Media (All files)
/scripts (All files)
/usn (All files)
/views (All files)
/error.html
/favicon.ico


Customising your uSkinned Theme
****************************************************************
We recommend that you do not edit the original files supplied with your uSkinned theme. Instead you should follow these steps to create your own theme files which you are free to edit:

Step 1: Decide on the name of your custom theme, preferably one word, for example 'Custom1'
Step 2: Create a copy of the usn_fabric folder within /css, /less, /scripts, /views/partials
Step 3: Place your copied folders in these 4 folders and rename to the name of your theme, for example '/css/usn_custom1'. Make sure you prefix with 'usn_'
Step 4: Update file /config/usntheme.config' adding a new item for your theme:

<add name="Custom1" smallLogoHeight="60" largeLogoHeight="80" version="1.0" />

You are now safe to edit your new theme which will be available within Umbraco with the name 'Custom1'

Within the content section of Umbraco, go to one of the styles below the 'Website Styles' node. You will be able to select your new theme from the 'Selected theme' field. 

Upgrading your uSkinned Theme to latest verion
****************************************************************
Occasionally we will release updates to your uSkinned Theme which may contain bug fixes or new features. The Theme Updates log for this theme can be found here:

https://uskinned.net/themes/fabric/

Unfortunately we cannot provide an automated update process as we have no way of knowing how you may customise your chosen theme. There would be a danger that any changes you have made would be overwritten.

The updates log will notify you of what changes have been made between versions.

We will release separate package files containing updates which will be in the /updates folder of your website. You can use the files within this folder to compare against your live website files for changes.

A popular tool for comparing changes can be found here:

https://winmerge.org/

Minor version updates (0.01 > 0.02) will involve only file changes and updates can be achieved by copying the changed files into your current website.

Medium version updates (0.10 > 0.20) may involve in addition to file change updates, updates to Document Types or Data Types. Instructions will be provided on what has been changed and what will need to be added manually to your website.

Major version updates (1.0 > 2.0) involve significant changes to your uSkinned theme and there will be no easy upgrade process. Major version changes are essentially a brand new theme. If you wish to use new features and there is no easy upgrade path then you should install a new version of your theme and then manually move content from your old site into the new site.