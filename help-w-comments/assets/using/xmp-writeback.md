---
title: XMP writeback to renditions
seo-title: XMP writeback to renditions
description: Learn how the XMP writeback feature propagates the metadata changes for an asset to all or specific renditions of the asset.
seo-description: Learn how the XMP writeback feature propagates the metadata changes for an asset to all or specific renditions of the asset.
uuid: 33cf91e6-6141-49fb-9d5b-39c74ebbc333
contentOwner: Chiradeep Majumdar
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
discoiquuid: 121c077a-7268-4c14-b316-e64f88b18cb1
index: y
internal: n
snippet: y
---

# XMP writeback to renditions{#xmp-writeback-to-renditions}

This XMP Writeback feature in Adobe Experience Manager (AEM) Assets replicates asset metadata changes to the renditions of the asset.

When you change the metadata for an asset from within AEM Assets or while uploading the asset, changes are initially stored within the asset node in Crx-De.

The XMP Writeback feature propagates the metadata changes to all or specific renditions of the asset.

Consider a scenario where you modify the Title property of the asset titled "**Classic Leather**" to "**Nylon**."

![](assets/metadata.png)

In this case, the AEM Assets saves the changes to the **Title** property in the `dc:title` parameter for the asset metadata stored in the asset hierarchy.

![](assets/metadata_stored.png)

However, AEM Assets does not automatically propagate any metadata changes to the renditions of an asset.

The XMP Writeback feature lets you propagate the metadata changes to all or specific renditions of the asset. However, the changes are not stored under the metadata node in the asset hierarchy. Instead, this feature embeds the changes in the binary files for the renditions.

## Enabling XMP writeback {#enabling-xmp-writeback}

To enable the metadata changes to be propagated to the renditions of the asset when uploading it, modify the **Adobe CQ DAM Rendition Maker** configuration in Configuration Manager.

1. Open Configuration Manager from *http://&lt;Server&gt;:&lt;Port&gt;/system/console/configMgr*.
1. Open the **Adobe CQ DAM Rendition Maker** configuration.
1. Select the **Propagate XMP** option, and then save the changes. 

   ![](assets/chlimage_1-349.png)

## Enabling XMP writeback for specific renditions {#enabling-xmp-writeback-for-specific-renditions}

To let the XMP Writeback feature propagate metadata changes to select renditions, specify these renditions to the XMP Writeback Process workflow step of DAM Metadata WriteBack workflow. By default, this step is configured with the original rendition.

For the XMP Writeback feature to propagate metadata to the rendition thumbnails 140.100.png and 319.319.png, perform these steps.

1. Tap/click the AEM logo, and then navigate to **Tools** &gt; **Workflow** &gt; **Models**.
1. From the Models page, open the **DAM Metadata Writeback** workflow model.
1. In the **DAM Metadata Writeback** properties page, open the **XMP Writeback Process** step.
1. In the Step Properties dialog box, tap/click the **Process** tab.
1. In the **Arguments** box, add `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, andd then tap/click **OK**.

   ![](assets/step_properties.png)

1. Save the changes.
1. To regenerate the pyramid TIF renditions for Dynamic Media images with the new attributes, add the **Dynamic Media Process Image Assets** step to the DAM Metadata Writeback workflow.
1. Save the workflow.

The metadata changes are propagated to the renditions renditions thumbnail.140.100.png and thumbnail.319.319.png of the asset, and not the others.

>[!NOTE]
>
>For XMP writeback issues in 64 bit Linux, see [How to enable XMP write-back on 64-bit RedHat Linux](http://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>For more information about supported platforms, see [XMP metadata write-back prerequisites](../../sites/deploying/using/technical-requirements.md#main-pars-title-9).

## Filtering XMP metadata {#filtering-xmp-metadata}

AEM Assets supports both blacklist and whitelist filtering of properties/nodes for XMP metadata that is read from asset binaries and stored in JCR when assets are ingested.

Blacklist filtering lets you import all XMP metadata properties except the properties that are specified for exclusion. However, for asset types such as INDD files that have huge amounts of XMP metadata (for example 1000 nodes with 10,000 properties), the names of nodes to be filtered are not always known in advance. If blacklist filtering allows a large number of assets with numerous XMP metadata to be imported, the AEM instance/cluster can encounter stability issues, for example clogged observation queues.

Whitelist filtering of XMP metadata resolves this issue by letting you define the XMP properties to be imported. This way, other/unknown XMP properties are ignored. You can add some of these properties to the blacklist filter for backward compatibility.

1. Open Configuration Manager from *http://&lt;Server&gt;:&lt;Port&gt;/system/console/configMgr*.
1. Open the **Adobe CQ DAM XmpFilter** configuration.
1. To apply whitelist filtering, select **Apply Whitelist to XMP Properties**, and specify the properties to be imported in the **Whitelisted XML Names for XMP filtering** box.

   ![](assets/chlimage_1-350.png)

1. To filter out blacklisted XMP properties after applying whitelist filtering, specify them in the **Blacklisted XML Names for XMP filtering** box.

   >[!NOTE]
   >
   >The **Apply Blacklist to XMP Properties** option is selected by default. In other words, blacklist filtering is enabled by default. To disable blacklist filtering, unselect the **Apply Blacklist to XMP Properties** option.

1. Save the changes.
