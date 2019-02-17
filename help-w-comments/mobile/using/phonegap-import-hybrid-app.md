---
title: Import an existing hybrid app
seo-title: Import an existing hybrid app
description: A sample app has been created that demonstrates all of the new features in AEM Mobile to support migrating an existing PhoneGap app into AEM as well as valid app structure.
seo-description: A sample app has been created that demonstrates all of the new features in AEM Mobile to support migrating an existing PhoneGap app into AEM as well as valid app structure.
uuid: 6170515c-dbd8-4df1-bc77-c630b7e91ae6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: 54110bba-66e0-4b46-86cf-06979007f6ee
redirecttarget: /content/help/en/experience-manager/6-4/mobile/using/phonegap-adding-content-to-imported-app
index: y
internal: n
snippet: y
---

# Import an existing hybrid app{#import-an-existing-hybrid-app}

>[!NOTE]
>
>Adobe recommends using the SPA Editor for projects that require single page application framework-based client-side rendering (e.g. React). [Learn more](../../sites/developing/using/spa-overview.md).

### The Hybrid App Sample {#the-hybrid-app-sample}

A [sample app](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) has been created that demonstrates all of the new features in AEM Mobile to support migrating an existing PhoneGap app into AEM as well as valid app structure.

### Importing a Hybrid App {#importing-a-hybrid-app}

This feature is great for bootstrapping an app in AEM and for demos. Proper AEM package management techniques should still be used before moving an app to production. Any existing PhoneGap app that has been zipped up can be imported into AEM Mobile.

The import process is fully automated and takes care of copying the content to the correct location and setting up the correct app instance properties. A new app will also be created if an existing one cannot be found. An existing app will need to have an **app-assets** handler already but this handler will be included with new apps.

Dragging the zipped app onto the AEM Mobile apps catalog will automatically start the import process as shown below.

![](assets/chlimage_1-41.png)

### The Next Steps {#the-next-steps}

See the following resources to learn more about other authoring roles:

* [The Manage App Tile](../../mobile/using/phonegap-app-details-tile.md)
* [Editing App Metadata](../../mobile/using/phonegap-editmetadata.md)
* [App Definitions](../../mobile/using/phonegap-app-definitions.md)
* [Creating a New App using Create App Wizard](../../mobile/using/phonegap-create-new-app.md)
* [Content Services](/mobile/using/content-as-a-service) [](/mobile/using/content-as-a-service)

### Additional Resources {#additional-resources}

To learn about the roles and responsibilities of an Adminstrator and Developer, see the resources below:

* [Developing for Adobe PhoneGap Enterprise with AEM](../../mobile/using/developing-in-phonegap.md)
* [Administering Content for Adobe PhoneGap Enterprise with AEM](../../mobile/using/administer-phonegap.md)
