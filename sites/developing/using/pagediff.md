---
title: Developing and Page Diff
seo-title: Developing and Page Diff
description: null
seo-description: null
uuid: 3858a30b-5669-4b53-a61b-d1843a8cbdde
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: introduction
content-type: reference
discoiquuid: eda2b837-a032-4b3f-82f0-2bb757ce81e5
isreadyforlocalization: false
index: y
internal: n
snippet: y
---

# Developing and Page Diff{#developing-and-page-diff}

## Feature Overview {#feature-overview}

Content creation is an iterative process. Authoring with efficiency requires being able to see what has changed from one iteration to another. Viewing one page version and then the other is inefficient and prone to error. An author wants to be able to compare the current page to a previous version side-by-side with the differences highlighted.

The page diff allows a user to compare the current page to launches, previous versions, etc. For details of this user feature, see [Page Diff](../../authoring/using/page-diff.md).

## Operation Details {#operation-details}

When comparing versions of a page, the previous version(s) that the user wishes to compare is/are recreated by AEM in the background in order to facilitate the diff. This is needed to be able to render the content for side-by-side comparison.

When content is compared, the whole tree up to the page to compare is recreated in the following location:

`/content/versionhistory/<userId>/<site structure>`

This recreation operation is done by AEM internally and is transparent to the user and requires no intervention. However an administrator viewing the repository for example in CRX DE Lite would see these recreated versions within the content structure.

## Permissions {#permissions}

Because when using the page diff mechanism, [AEM recreates the previous version of the page,](../../developing/using/pagediff.md#main-pars-header) in order to use the feature the user must have certain JCR permissions.

>[!CAUTION]
>
>In order to use the page diff feature, the user needs to have the** Modify/Create/Delete** permission on the node `/content/versionhistory`.

## Developer Limitations {#developer-limitations}

Previously, in Classic UI, special development consideration had to be made to facilitate AEM diffing (such as using `cq:text` tag lib, or custom integrating the `DiffService` OSGi service into components). This is no longer needed for the new diff feature, since the diff occurs client-side via DOM comparison.

However there are a number of limitations that need to be considered by the developer.

* This feature uses CSS classes that are not name spaced to the AEM Product. If other custom CSS classes or 3rd party CSS classes with the same names are included on the page, the display of the diff may be affected.

    * `html-added`
    * `html-removed`
    * `cq-component-added`
    * `cq-component-removed`
    * `cq-component-moved`
    * `cq-component-changed`

* Because the diff is client-side and executes on page load, any adjustments to the DOM after the client-side diff service has run will not be accounted for. This may affect

    * Components that use AJAX to inlcude content
    * Single Page Applications
    * Javascript based components that manipulate the DOM upon user interaction.
