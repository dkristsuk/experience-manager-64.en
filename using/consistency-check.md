---
title: Consistency and Traversal Checks
seo-title: Consistency and Traversal Checks
description: null
seo-description: Learn how to perform consistency and traversal checks.
uuid: 43ba4951-3952-4bd3-bb29-6872e3712dcf
content-encoding: ISO-8859-1
aemsrcnodepath: /content/help/en/experience-manager/6-4/sites/deploying/using/consistency-check
contentOwner: User
cq-designpath: /etc/designs/help
cq-lastmodified: 2018-04-30T03 26 44.787-0400
cq-lastmodifiedby: carlino
cq-lastreplicated: 2018-04-03T08 40 19.650-0400
cq-lastreplicatedby: carlino
cq-lastreplicationaction: Activate
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
cq-template: /apps/help/templates/article-3
discoiquuid: 1ee8a7b3-6e32-4266-851d-77d756645f6c
firstPublishExternalDate: 2018-04-03T08:40:18.851-0400
isreadyforlocalization: false
jcr-created: 2017-12-01T19 04 04.593-0500
jcr-createdby: admin
jcr-ischeckedout: true
jcr-language: en_us
lastPublishExternalDate: 2018-04-03T08:40:18.851-0400
lochandoffdate: 2018-04-30T03 26 44.787-0400
lr-lastreplicatedby: carlino@adobe.com
mwpw-migration-script-version: 2017-10-12T21 46 58.665-0400
navTitle: Consistency and Traversa Checks
primaryAudienceTag: audience:deploying
primaryProductTag: products:SG_EXPERIENCEMANAGER/6.4/SITES
publishexternaldate: 2018-04-03T08 40 18.851-0400
publishExternalURL: https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/consistency-check.html
qaDate: 2017-10-12T21:46:00.000-0400
qaNotes: /content/docs/en/aem/6-3/deploy/upgrade/consistency-check
sha1: 9cea98e5f489ce03bfccc1cf8077fbb6e348faf1
topicBrowsingSortDate: 2018-04-03T08:40:18.851-0400
index: y
internal: n
snippet: y
translate: y
---

# Consistency and Traversal Checks

When upgrading there can be problems due to workspace inconsistencies. You can either run a test upgrade to see if this will be an issue, or run the consistency checks as preventive action.

If you run a test upgrade that fails due to workspace inconsistencies you will see entries similar to the following in crx-quickstart/logs/crx/error.log:

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

### Perform a Consistency Check

To perform a consistency check, navigate to the administration page for the JMX Mbean** com.adobe.granite (Repository)**. From the AEM main screen, go to:

**Tools &gt; Web Console &gt; Main(on menu bar) &gt; JMX &gt; com.adobe.granite (Repository)**

On a default installation, it is found here: ** [|Show Me|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

In the **Operations** section of the page you will find two methods: **`traversalCheck`** and **`consistencyCheck`**. To execute a check, click on the operation and enter the desired parameters.
![](assets/chlimage_1.png) 