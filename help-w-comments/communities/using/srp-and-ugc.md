---
title: SRP and UGC Essentials
seo-title: SRP and UGC Essentials
description: Storage resource provider and user-generated content overview
seo-description: Storage resource provider and user-generated content overview
uuid: c4523d64-7793-4e13-b991-a534651d563e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 923e397d-5dcf-4cbc-b0fa-92815a69bc93
index: y
internal: n
snippet: y
---

# SRP and UGC Essentials{#srp-and-ugc-essentials}

## Introduction {#introduction}

If unfamiliar with the storage resource provider (SRP) and its relationship to user-generated content (UGC), visit [Community Content Storage](../../communities/using/working-with-srp.md) and [Storage Resource Provider Overview](../../communities/using/srp.md).

This section of the documentation provides some essential information about SRP and UGC.

## StorageResourceProvider API {#storageresourceprovider-api}

The SocialResourceProvider API (SRP API) is an extension of various Sling Resource Provider APIs. It includes support for pagination and atomic increment (useful for tally and scoring).

Queries are necessary for SCF components as there is the need to sort by date, helpfulness, number of votes, and so on. All SRP options have flexible query mechanisms which do not rely on bucketing.

The SRP storage location incorporates the component path. The SRP API should always be used to access UGC as the root path depends on the SRP option selected, such as ASRP, MSRP, or JSRP.

The SRP API is not an abstract class, it is an interface. A custom implementation should not be undertaken lightly, as the benefits of future improvements to internal implementations would be missed when upgrading to a new release.

The means for using the SRP API are through provided utilities, such as those found in the SocialResourceUtilities package.

When upgrading from AEM 6.0 or earlier, it will be necessary to migrate UGC for all SRPs, for which an Open Source tool is available. See [Upgrading to AEM Communities 6.3](../../communities/using/upgrade.md).

>[!NOTE]
>
>Historically, utilities for accessing UGC were found in the SocialUtils package, which no longer exists.
>
>For replacement utilities, see [SocialUtils Refactoring](../../communities/using/socialutils.md).

## Utility Method to Access UGC {#utility-method-to-access-ugc}

To access UGC, use a method from the SocialResourceUtilities package that returns a path suitable for accessing UGC from SRP and replaces the deprecated method found in the SocialUtils package.

Following is a minimal example of using the resourceToUGCStoragePath() method in a servlet :

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String ugcPath = socialResourceUtilities.resourceToUGCStoragePath(request.getResource());
  // rest of servlet
}
```

For other SocialUtils replacements, see [SocialUtils Refactoring](../../communities/using/socialutils.md).

For coding guidelines, visit [Accessing UGC with SRP](../../communities/using/accessing-ugc-with-srp.md).

>[!CAUTION]
>
>The path resourceToUGCStoragePath() returns is *not *suitable for [ACL checking](../../communities/using/srp.md#foraccesscontrolacls).

## Utility Method to Access ACLs {#utility-method-to-access-acls}

Some SRP implementations, such as ASRP and MSRP, store community content in databases which provide no ACL verification. Shadow nodes provide a location in the local repository to which ACLs can be applied.

Using the SRP API, all SRP options perform the same check of the shadow location prior to all CRUD operations.

To check ACLs, use a method that returns a path suitable for checking the permissions applied to the resource's UGC.

Following is a simple example of using the resourceToACLPath() method in a servlet :

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String aclPath = socialResourceUtilities.resourceToACLPath(request.getResource());
  // rest of servlet
}
```

>[!CAUTION]
>
>The path returned by resourceToACLPath() is *not *suitable for [accessing the UGC](#utilitymethodtoaccessacls) itself.

## UGC-Related Storage Locations {#ugc-related-storage-locations}

The following descriptions of storage location may be of help when developing with JSRP or perhaps MSRP. There is currently no UI to access UGC stored in ASRP, as there is for JSRP ([CRXDE Lite](../../sites/developing/using/developing-with-crxde-lite.md)) and MSRP (MongoDB tools).

**component location**

When a member enters UGC in the publish environment, they are interacting with a component as part of an AEM site.

An example of such a component is the [comments component](http://localhost:4502/content/community-components/en/comments.html) that exists in the [Community Components Guide](../../communities/using/components-guide.md) site. The path to the comment node in the local repository is :

* component path = */content/community-components/en/comments/jcr:content/content/includable/comments*

**shadow node location**

The creation of UGC also creates a [shadow node](../../communities/using/srp.md#aboutshadownodesinjcr) to which the necessary ACLs are applied. The path to the corresponding shadow node in the local repository is the result of prepending the shadow node root path to the component path :

* root path = /content/usergenerated
* comment shadow node = /content/usergenerated*/content/community-components/en/comments/jcr:content/content/includable/comments*

**UGC location**

The UGC is created in neither of those locations, and should only be accessed using an [utility method](#utilitymethodtoaccessugc) which invokes the SRP API.

* root path = /content/usergenerated/asi/*&lt;srp-choice&gt;*
* UGC node for JSRP = /content/usergenerated/asi/jcr*/content/community-components/en/comments/jcr:content/content/includable/comments*/srzd-let_it_be_

*Be aware*, for JSRP, the UGC node will *only *be present on the AEM instance (either author or publish) on which it was entered. If entered on a publish instance, moderation will not be possible from the moderation console on author.

<!--
Comment Type: draft

<h2>SRP Tools</h2>
-->

<!--
Comment Type: draft

<p>The customer can use an opensource tool to clean their report suites. The tool is here:</p>
<p><a href="https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools">https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools</a></p>
<p>The customer can self-manage their report suites. We don’t yet have a UI to manage UGC, but the source to the command line tool is available in that repo if the customer would like to fork and enhance it</p>
-->

## Related Information {#related-information}

* [Storage Resource Provider Overview](../../communities/using/srp.md) - introduction and repository usage overview
* [Accessing UGC with SRP](../../communities/using/accessing-ugc-with-srp.md) - coding guidelines
* [SocialUtils Refactoring](../../communities/using/socialutils.md) - mapping deprecated utility methods to current SRP utility methods
