---
title: Managing Collections
seo-title: Managing Collections
description: Understand the concept of collection in AEM Assets. Learn how to collections, manage, edit, and collections with other users.
seo-description: Understand the concept of collection in AEM Assets and learn how you can share collections with other users.
uuid: adee5a3b-02e6-44a4-9de5-2bf03d84921b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
content-type: reference
topic-tags: authoring
discoiquuid: 86468a3d-45c0-41a5-80bc-1b29acf672df
index: y
internal: n
snippet: y
---

# Managing Collections{#managing-collections}

Understand the concept of collection in AEM Assets. Learn how to collections, manage, edit, and collections with other users.

A collection is a set of assets within Adobe Experience Manager (AEM) Assets. Use collections to share assets between users.

* A collection can include assets from different locations.
* You can share collections with various users that are assigned different levels of privileges, including viewing, editing, and so on.

You can share multiple collections with a user. Each collection contains references to assets. The referential integrity of assets is maintained across collections.

Collections are of the following types, based on the way they collate assets:

* A collection that contains a **static reference list** of assets, folders, and other collections  

* A **Smart collection** that dynamically includes assets based on a search criteria

## Navigating the Collections console {#navigating-the-collections-console}

To open the **Collections** console:

1. Tap or click the AEM logo.
1. From the Navigation page, go to **Assets **&gt; **Collections**. The **Collections** console is displayed.

## Creating a collection {#creating-a-collection}

You can create a collection either with [static references](#creatingacollectionwithstaticreferences) or based on a [search criteria-based filter](#creatingacollectionwithsearchcriteriabasedfilteralsocalledsmartcollection). You can also create a collection from a lightbox.

### Creating a collection with static references {#creating-a-collection-with-static-references}

You can create a collection with static references, for example a collection with references to assets, folders, collections, spin sets, and image sets.

1. Navigate to the **Collections** console.
1. From the toolbar, tap/click **Create**.
1. In the **Create Collection** page, enter a title and an optional description for the collection.
1. Add members to the collection and assign appropriate permissions. Alternatively, select **Public Collection** to allow all users to access the collection.

   >[!NOTE]
   >
   >To enable the members to share collections with other users, provide the `dam-users` group read permissions at the path `home/users`. Give permission to the users at `/content/dam/collections` location to allow the users to view the Collections in pop up lists. Alternatively, make the user a part of `dam-users` group.

1. (Optional) Add a thumbnail image for the collection.
1. Tap/click **Create**, and then tap/click **OK** to close the dialog. A collection with the specified title and properties is opened in the Collections console.

   >[!NOTE]
   >
   >AEM Assets lets you create review tasks for a collection similar to the way you create review tasks for an assets folder.

   To add assets to the collection, navigate to the Assets user interface. For details, see [Adding assets to a collection](../../assets/using/managing-collections-touch-ui.md#main-pars-title-0).

### Create collections using Dropzone {#create-collections-using-dropzone}

You can drag assets from the Assets UI to a collection. You can also create a copy of a collection and drag the assets there.

1. From the Assets UI, select the assets you want to add to a collection.
1. Drag the assets to the **Drop in Collection** zone.

   ![](assets/drop_in_collection.png)

   Release the mouse button when the Dropzone becomes active, and its label changes to **Drop to Add**.

   ![](assets/drop_to_add.png)

   Alternatively, tap/click the **To Collection** icon from the toolbar.

   ![](assets/chlimage_1-111.png)

1. In the **Add To Collection** page, tap/click the **Create Collection** icon from the toolbar.

   If you want to add the assets to an existing collection, select it from the page, and tap/click **Add**. By default, the most recently updated collection is selected.

1. In the **Create New Collection** dialog, specify a name for the collection. If you want the collection to be accessible to all users, select **Public Collection**.
1. Tap/click **Continue** to create the collection.

### Creating a smart collection {#creating-a-smart-collection}

A smart collection uses a search criteria to dynamically populate assets. To create a smart collection:

1. Navigate to the** Assets **UI, and tap/click the** Search** icon.

   ![](assets/chlimage_1-112.png)

1. With the cursor in the Omni Search box, press the Return key. 

   ![](assets/chlimage_1-113.png)

1. Tap/click the GlobalNav icon to display the Filters panel.
1. In the Omni Search box, enter the search keywords and then select a search criteria from the Search panel. For example, to search for assets that include "Surfing" in the title, enter "Surfing" in the Omni Search box and then press Enter.
1. From the **Files & Folders** list, select **Files**.

   ![](assets/files_option.png)

1. Tap/click **Save Smart Collection**.
1. Specify a name for the collection. Select **Public** to add the DAM Users group with the Viewer role to the smart collection.

   ![](assets/save_collection.png)

   >[!NOTE]
   >
   >If you select **Public**, the smart collection becomes available to everyone with the Owner role after you create it.

   >[!NOTE]
   >
   >If you deselect the **Public** option, the DAM user group is no longer associated with the smart collection.

1. Tap/click **Save** to create the smart collection, and then close the message box to complete the process.

   The new smart collection is also added to the **Saved Searches** list.

   ![](assets/collection_listing.png)

   The label of the **Create Smart Selection** button changes to **Edit Smart Selection**. To edit the settings of the smart collection, select **Files** from the **Files & Folders** list. Then, tap/click the **Edit Smart Selection** button.

   ![](assets/chlimage_1-114.png)

>[!NOTE]
>
>If you make a smart collection public after upgrading from AEM 5.6.1 to AEM 6.2, it becomes available to everyone with the Owner role.

## Adding assets to a collection {#adding-assets-to-a-collection}

You can add assets to a collection that contains a list of referenced assets or folders.

>[!NOTE]
>
>Smart collections use a search query to populate assets. Therefore, static references to assets and folders are not applicable to them.

1. In the Assets UI, navigate to the location of the asset that you want to add to a collection.
1. Select the asset and tap/click the **To Collection** icon from the toolbar.

   ![](assets/chlimage_1-115.png)

   Alternatively, you can drag the asset to the **Drop in Collection** zone. Release the mouse button when the drop zone becomes active and its label changes to **Drop to Add**.

1. In the **Add To Collection** page, select the collection to which you want to add the asset.
1. Tap/click **Add**, and then close the confirmation message. The asset is added to the collection.

## Editing a smart collection {#editing-a-smart-collection}

Smart collections are built by saving a search so you can alter their content by modifying the search parameters of the [saved search](#editingsavedsearches).

1. In the** Assets **UI, tap/click the** Search** icon from the toolbar.

   ![](assets/chlimage_1-116.png)

1. With the cursor in the Omni Search box, press the Return key. 
1. Tap/click the GlobalNav icon to display the Filters panel.
1. From the **Saved Searches** list, select the smart collection you want to modify. The Search panel displays the filters configured for the saved search.

   ![](assets/select_smart_collection.png)

1. From the **Files & Folders** list, select **Files**.
1. Modify one or more filters, as necessary. Tap/click **Edit Smart Collection**.

   You can also edit the name of the smart collection.

   ![](assets/edit_smart_collectiondialog.png)

1. Tap/click **Save**. The **Edit Smart Collection** dialog appears.
1. Tap/click **Overwrite** to replace the original smart collection with the edited collection. Alternatively, select **Save As** to save the edited collection separately.
1. In the confirmation dialog, tap/click **Save** to complete the process.

## Viewing and editing collection metadata {#viewing-and-editing-collection-metadata}

Collection metadata comprises data about the collection, including any tags that are added.

1. From the Collections console, select a collection and tap/click the **Properties **icon from the toolbar.
1. In the **Collection Metadata **page, view the collection metadata from the **Basic** and **Advanced** tabs.
1. Modify the metadata, as necessary, and then tap/click **Save & Close** from the toolbar to save the changes.

### Editing collection metadata in bulk {#editing-collection-metadata-in-bulk}

You can edit the metadata of multiple collections simultaneously. This functionality helps you quickly replicate common metadata in multiple collections.

1. In the Collections console, select two or more collections for which you want to edit metadata.
1. From the toolbar, tap/click the **Properties** icon.
1. In the **Collection Metadata** page, edit the metadata under the **Basic** and **Advanced** tabs, as necessary.
1. Tap/click **Save & Close ** from the toolbar, and then close the confirmation dialog to complete the process.
1. To append the new metadata with the existing metadata, select **Apend mode**. If you do not select this option, the new metadata replaces the existing metadata in the fields. Tap/click **Submit**.

   >[!NOTE]
   >
   >The Append mode works only for fields that can contain multiple values. For fields that can contain only a single value, the new metadata is not appended to the existing value in the field even if you select **Append mode**.

## Searching {#searching}

The Search feature within Collections supports both [Searching for Collections](#searchingcollections) and [Searching for assets within a Collection](#searchingwithincollections).

#### Searching Collections {#searching-collections}

You can search collections from the Collections console. When you search with keywords in the Omni Search box, AEM Assets searches for collection names, metadata, and the tags added to the collections.

#### Searching within Collections {#searching-within-collections}

In the Collections console, tap/click a collection to open it.

Within a collection, AEM Asset search is restricted to assets (and their tags and metadata) within the collection that you are viewing.

### Editing Collection Settings {#editing-collection-settings}

You can edit collection settings, such as title and description, or to add members to a collection.

1. Select a collection, and tap/click the **Settings** icon in the toolbar. Alternatively, use the **Settings** quick action from the collection thumbnail.
1. Modify the collection settings in the **Collection Settings** page. For example, modify the collection title, descriptions, members, and permissions as discussed in [Adding Collections](#main-pars-title).   

1. Tap/click **Save** to save the changes.

   ![](assets/chlimage_1-117.png)

## Deleting a collection {#deleting-a-collection}

1. From the Collections console, select one or more collections and tap/click the** Delete** icon in the toolbar.

   ![](assets/chlimage_1-118.png)

1. In the dialog, tap/click **Delete** to confirm the delete action.

   >[!NOTE]
   >
   >You can also detete Smart collections by [deleting saved searches](#deletingsavedsearches).

## Downloading a collection {#downloading-a-collection}

When you download a collection, the entire hierarchy of assets within the collection is downloaded, including folders and child collections.

1. From the Collections console, select one or more collections to download.
1. From the toolbar, tap/click the** Download** icon.
1. In the **Download **dialog, tap/click **Download**. If you want to download the renditions of the assets within the collection, select **Renditions**. Select the **Email** option to send an email notification to the owner of the collection.

   When you select a collection to download, the complete folder hierarchy under the collection is downloaded. To include each collection you download (including assets in child collections nested under the parent collection) in an individual folder, select **Create separate folder for each asset**.

## Creating nested collections {#creating-nested-collections}

You can add a collection to another collection, thereby creating a nested collection.

1. From the Collections console, select the desired collection or group of collections, and tap or click the **To Collection** icon in the toolbar.

   ![](assets/chlimage_1-119.png)

1. From the **Add To Collection** page, select the collection in which to add the collection.

   >[!NOTE]
   >
   >The most recently updated collection is selected by default in the **Add To Collection** page.

1. Tap/click **Add**. A message confirms that the collection is added to the target collection in the **Select Destination** page. Close the message to complete the process.

>[!NOTE]
>
>Smart collections cannot be nested. In other words, Smart collections cannot contain any other collection.

## Saved searches {#saved-searches}

In the Assets UI, you can search or filter assets based on certain rules, search criteria, or custom search facets. If you save these as **Saved Searches**, you can access them later from the **Saved Searches** list in the Filter panel. Creating a saved search also creates a smart collection.

![](assets/saved_searches_list.png) 

### Creating Saved Searches {#creating-saved-searches}

Saved searches are created when you create a smart collection. Smart collections are automatically added to the **Saved Searches** list. The Saved Searches query for the collection is saved in the `dam:query` property in crxde at the relative location */content/dam/collections/*. [](#creatingasmartcollection)

>[!NOTE]
>
>You can share smart collections in the same way as you share static collections.

### Editing Saved Searches {#editing-saved-searches}

Editing saved searches is the same as editing smart collections. For details, see [Editing a smart collection](../../assets/using/managing-collections-touch-ui.md#main-pars-title-5).

### Deleting Saved Searches {#deleting-saved-searches}

1. Navigate to the **Assets** UI, and tap/click the** Search** icon on the toolbar.

   ![](assets/chlimage_1-120.png)

1. With the cursor in the Omni Search box, press the Return key.
1. Click or tap the GlobalNav icon to display the Filters panel.  

1. From the **Saved Searches** list, tap/click the **Delete** icon next to the smart collection you want to delete.

   ![](assets/select_smart_collection-1.png)

1. In the dialog, tap/click **Delete** to delete the saved search.

## Running a workflow on a collection {#running-a-workflow-on-a-collection}

You can run a workflow for the assets within a collection. If the collection contains nested collections, the workflow also runs on the assets within the nested collections. However, if the collection and the nested collection contain duplicate assets, the workflow only runs once for such assets.

1. From the Collections console, select a collection on which you want to run a workflow.
1. Tap/click the GlobalNav icon, and choose **Timeline** from the list.
1. From the timeline, click or tap the Caret icon at the bottom, and then tap/click **Start Workflow**.

   ![](assets/chlimage_1-121.png)

1. In the **Start Workflow** section, select a workflow model from the list. For example, select the **DAM Update Asset** model.
1. Enter a title for the workflow, and tap/click **Start**.
1. In the dialog, tap/click **Proceed**. The workflow runs on all the assets in the collection.

## See also {#see-also}

* [Configure AEM Assets email notifications](../../sites/administering/using/notification.md#assetsconfig)
* [Edit metadata properties of multiple Collections](../../assets/using/managing-multiple-assets.md)
* [Create a review task for Collections](../../assets/using/bulk-approval.md)
