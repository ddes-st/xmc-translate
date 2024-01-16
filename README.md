# Sitecore XMC & OpenAI Translation Accelerator

## Prerequisites

Before proceeding:
- Make sure your computer has Node.js installed: https://ionicframework.com/docs/reference/glossary#node
- Make sure you have access to Sitecore Customer Portal: https://portal.sitecorecloud.io/
- Make sure your organization includes a Sitecore XM Cloud entitlement
- Make sure your organization includes a Sitecore Connect entitlement

In the repository, you will find:
- The 'xmc-explore-app.zip' archive: it contains a Next.js application that connects to XM Cloud, retrieves and shows site content, offers to switch languages, and provides options to edit content fields as well as sends OpenAI to translate.
- The 'xm-cloud-management_auto_translate_manifest.zip' archive: it contains 2 connections and an 'Auto Translate' recipe packaged into a manifest that can be imported into Sitecore Connect. The recipe listens to some XMC Webhook requests, checks the content item type and if it recognizes it, sends content to OpenAI for translation before persisting the results back into XM Cloud.

Please note that the two archives / apps are not connected with each other. The Next.js App connects to Open AI directly. The Connect project expects XM Cloud to send content payload to trigger the job / recipe. 

## XMC Explore App

Basic instructions to run the application are provided as part of the app README file.

Update the .env files with your own XM Cloud and OpenAI details

Run the application

Explore code

## Sitecore Connect Manifest

Create a Project for this initiative

Import the .Zip archive into your project in Sitecore Connect via
```
Tools / Recipe Lifecycle Management / Import
```

Go to and fill in the XM Cloud & OpenAI Connections settings that have been created within your project

Go to and review the flow of the Automatic Translation Recipe. You will notice that this is a recipe that is looking for a News content item type prior to moving forward. The recipe ignores any other type. You will need to make this recipe generic to accommodate your needs.

Note 1: we have packaged a custom connector that manages the connection and operations with XM Cloud. This is available under Tools > Connector SDK > Sitecore XM Cloud. Take the time to understand how how it has been built, ups and down. The core of the work will be to customize this connector.

Note 2: the created environment property (under Tools > Environment Properties > Content_Item_Template_ID) is being used in the Auto Translate recipe to offer some simple control to filter in and out content from the recieved payload. This should be ignored or customized as part of a generic translation use case.