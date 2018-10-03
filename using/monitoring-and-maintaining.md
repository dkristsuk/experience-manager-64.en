---
title: Monitoring and Maintaining Your CQ instance
seo-title: Monitoring and Maintaining Your CQ instance
description: null
seo-description: Learn how to monitor AEM.
uuid: ba60ab25-1d59-425e-90b9-2bb86c0be00a
content-encoding: ISO-8859-1
aemsrcnodepath: /content/help/en/experience-manager/6-4/sites/deploying/using/monitoring-and-maintaining
contentOwner: User
converted: true
cq-designpath: /etc/designs/help
cq-lastmodified: 2018-04-30T03 27 29.987-0400
cq-lastmodifiedby: carlino
cq-lastreplicated: 2018-04-03T08 43 27.978-0400
cq-lastreplicatedby: carlino
cq-lastreplicationaction: Activate
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: configuring
content-type: reference
cq-template: /apps/help/templates/article-3
discoiquuid: 62dbe161-5bb4-406f-a06e-63d66a2e0515
firstPublishExternalDate: 2017-10-31T16:17:53.997-0400
isreadyforlocalization: false
jcr-created: 2017-12-01T19 03 13.229-0500
jcr-createdby: admin
jcr-ischeckedout: true
jcr-language: en_us
jcr-lastmodifiedby: remove-legacypath-6-1
lastPublishExternalDate: 2018-04-03T08:43:26.619-0400
lochandoffdate: 2018-04-30T03 27 29.987-0400
lr-lastreplicatedby: carlino@adobe.com
moreHelpPaths: /content/help/en/experience-manager/6-4/sites/deploying/morehelp/configuring;/content/help/en/experience-manager/6-4/sites/deploying/morehelp/configuring
mwpw-migration-script-version: 2017-10-12T21 46 58.665-0400
navTitle: Monitoring and Maintaining Your CQ instance
primaryAudienceTag: audience:deploying
primaryProductTag: products:SG_EXPERIENCEMANAGER/6.4/SITES
publishexternaldate: 2018-04-03T08 43 26.619-0400
publishExternalURL: https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/monitoring-and-maintaining.html
qaDate: 2017-10-12T21:46:00.000-0400
qaNotes: /content/docs/en/aem/6-3/deploy/configuring/monitoring-and-maintaining
sha1: d27e12c0dbbc2603d8cc0042cf229b266a50fc8a
topicBrowsingSortDate: 2018-04-03T08:43:26.619-0400
index: y
internal: n
snippet: y
translate: y
---

# Monitoring and Maintaining Your CQ instance

After your CQ instances have been deployed certain tasks will be needed to monitor and maintain their operation, performance and integrity.

A key factor here is that to recognize potential issues you need to know how your systems looks and behaves under normal conditions. This is best done by monitoring the system and collecting information over a period of time.

| Check |Considerations |Comment / Actions |
|---|---|---|
| Backup plan. |  |See how to [Backup your CQ Instance](monitoring-and-maintaining.md#Backups). |
| Disaster recovery plan. |Your company's disaster recovery guidelines. |  |
| An error tracking system is available for reporting problems. |For example, [bugzilla](http://www.bugzilla.org/), [jira](http://www.atlassian.com/software/jira/), or one of many others. |  |
| File systems are being monitored. |The CRX repository will "freeze" if there is insufficient free disk space. It will resume once space becomes available. |" `*ERROR* LowDiskSpaceBlocker`" messages can be seen in the log file when free space becomes low. |
| [Log files](monitoring-and-maintaining.md#WorkingwithAuditRecordsandLogFiles) are being monitored. |  |  |
| System monitoring is (constantly) running in the background. |Including CPU, memory, disk and network usage. Using for example, iostat / vmstat / perfmon. |Logged data is visualized and can be used for tracking performance problems. Raw data is also accessible. |
| [CQ performance is being monitored](monitoring-and-maintaining.md#MonitoringPerformance). |Including [Request Counters](monitoring-and-maintaining.md#RequestCounters) to monitor traffic levels. |If a significant, or long term loss, of performance is seen, detailed investigation should be made. |
| You are monitoring your [Replication Agents](monitoring-and-maintaining.md#MonitoringYourReplicationAgents). `` |  |  |
| Regularly purge workflow instances. |Repository size and workflow performance. |See [Regular Purging of Workflow Instances](/content/help/en/experience-manager/6-4/sites/administering/using/workflows-administering#RegularPurgingofWorkflowInstances). |

---

## Backups

It is good practice to take backups of:

* Your software installation - before/after significant changes in the configuration
* The content held within the repository - regularly

Your company will probably have a backup policy that you will need to follow, additional considerations of what to backup and when include:

* how critical the system and data is.
* how often changes are made to either the software or data.
* volume of data; capacity can occasionally be an issue, as can the time needed to perform the backup.
* whether your backup can be made while users are online; and if possible, what is the performance impact.
* the geographical distribution of users; i.e. when is the best time to backup (to minimize impact)?
* your disaster recovery policy; are there guidelines on where the backup data has to be stored (e.g. offsite, specific medium, etc).

Often a full backup is taken at regular intervals (e.g. daily, weekly or monthly), with incremental backups in between (e.g hourly, daily or weekly).

>[!CAUTION]
>
><p>When implementing backups of your production instances, tests <i>must</i> be made to ensure that the backup can be successfully restored.<br> </p> <p>Without this, the backup is potentially useless (worst case scenario).<br> </p> 

>[!NOTE]
>
><p>For more information about backup performances, please read the <a href="/content/help/en/experience-manager/6-4/sites/deploying/using/configuring-performance.html#BackupPerformance">Backup Performance</a> section.</p>

### Backing up your software installation

After installation, or significant changes in the configuration, take a backup of your software installation.

To do this, you need to [back up your entire repository](#Backingupyourrepository) and then:

1. Stop CQ.

1. Back up the entire `<cq-installation-dir>` from your file system.

>[!CAUTION]
>
><p>If you are operating a cluster, then the &quot;shared&quot; folder may be in a different location and will also need to be backed up. See <a href="/content/help/en/DO NOT MIGRATE.html">How to Set Up a Cluster in CQ</a> for information about configuring a cluster.</p> 

>[!CAUTION]
>
><p>If you are operating a third-party application server, then additional folders may be in a different location and may also need to be backed up. See <a href="/content/help/en/experience-manager/6-4/sites/deploying/using/application-server-install.html">How to install AEM with an Application Server</a> for information about installing application servers.<a href="/content/docs/en/aem/6-3/deploy/installing.html#Installing Adobe Experience Manager with an Application Server"></a></p> 

>[!CAUTION]
>
><p>Incremental backup of the file data store is supported; when using incremental backup for other components (such as Lucene index), please ensure deleted files are also marked as deleted in the backup.</p> 

>[!NOTE]
>
><p>Disk mirroring can also be used as a backup mechanism.</p>

### Backing up your repository

The [Backup and Restore](/content/help/en/experience-manager/6-4/sites/administering/using/backup-and-restore) section of the CRX documentation covers all issues related to backups of the CRX repository.

For full details of making an online "hot" backup see [Creating an Online Backup](/content/help/en/experience-manager/6-4/sites/administering/using/backup-and-restore#OnlineBackup).

---

## Version Purging

The **Purge Versions** tool is intended for purging the versions of a node or a hierarchy of nodes in your repository. Its primary purpose is to help you reduce the size of your repository by removing old versions of your nodes.

This section deals with maintenance operations related to the versioning feature of CQ. The **Purge Version** tool is intended for purging the versions of a node or a hierarchy of nodes in your repository. Its primary purpose is to help you reduce the size of your repository by removing old versions of your nodes.

### Overview

The **Purge Versions **tool is available in the ** [Tools](/content/help/en/experience-manager/6-4/sites/administering/using/tools-consoles) console** under **Versioning** or directly at: ``

`http://<server>:<port>/etc/versioning/purge.html` 
![](assets/screen_shot_2012-03-15at14418pm.png) 

### Purging Versions of a Web Site

To purge versions of a web site, proceed as follows:

1. Navigate to the ** [Tools](/content/help/en/experience-manager/6-4/sites/administering/using/tools-consoles)** **console**, select **Versioning** and double-click **Purge Versions.**

1. Set the start path of the content to be purged (e.g. `/content/geometrixx-outdoors`).

    * If you want to only purge the node defined by your path, unselect **Recursive**.    
    * If you want to purge the node defined by your path and its descendants select **Recursive**.

1. Set the maximum number of versions (for each node) that you want to keep. Leave empty to not use this setting. 

1. Set the maximun version age in days (for each node) that you want to keep. Leave empty to not use this setting. 

1. Click **Dry Run** to preview what the purge process would do.

1. Click **Purge **to launch the process.

>[!CAUTION]
>
><p>Purged nodes can not be reverted without restoring the repository. You should take care of your configuration, so we recommend you to always perform a dry run before purging.<br> </p>

### Analyzing the Console

The **Dry Run** and **Purge** processes list all the nodes that have been processed. During the process, a node can have one of the following status:

* `ignore (not versionnable)`: the node does not support versioning and is ignored during the process.
* `ignore (no version)`: the node does not have any version and is ignored during the process. ``
* `retained`: the node is not purged.
* `purged`: the node is purged.

Moreover the console provides useful information about the versions:

* `V 1.0`: the version number.
* `V 1.0.1`*: the star indicates that the version is the current one.
* `Thu Mar 15 2012 08:37:32 GMT+0100`: the date of the version.

In the next example:

* The **Shirts **versions are purged because their version age is greater than 2 days.
* The **Tonga Fashions!** versions are purged because their number of versions is greater than 5.

![](assets/global_version_screenshot.png) 

---

## Working with Audit Records and Log Files

Auditing records and log files relating to Adobe Experience Manager (AEM) can be found at various locations. The following is provided to give you an overview of what you can find where.

#### Working with Logs

AEM WCM records detailed logs. After you unpack and start Quickstart, you can find logs in:

* `<*cq-installation-dir*>/crx-quickstart/logs/` ``
* `<*cq-installation-dir*>/crx-quickstart/repository/`

#### Log file rotation

Log file rotation refers to the process that limits the growth of file by creating new file periodically. In AEM, a log file called `error.log` will be rotated once a day according to the given rules:

* The `error.log` file is renamed according to the pattern {original_filename} `.yyyy-MM-dd`. For example on July 2010 11th, the current log file is renamed `error.log-2010-07-10`, then a new `error.og` is created.
* Previous log files are not deleted, so it is your responsibility to clean old log files periodically to limit the disk usage.

>[!NOTE]
>
><p>If you upgrade your AEM installation, note that any existing log file that is no more used by AEM will remain on the disk. You can remove them without risk. All new log entries will be written in the new log files.<br> </p>

### Finding the Log Files

Various log files are held on the file server where you installed AEM:

* `<*cq-installation-dir*>/crx-quickstart/logs`

    * `access.log` All access requests to AEM WCM and the repository are registered here.    
    * `audit.log` Moderation actions are registered here.    
    * `error.log` Error messages (of varying levels of severity) are registered here.    
    * [ `ImageServer-<PortId>-yyyy>-<mm>-<dd>.log`](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/c_image_server_log.html) This log is only used if dynamic media is enabled. It provides statistics and analytical information used for analyzing behavior of the internal ImageServer process.    
    * `request.log` Each access request is registered here together with the response.    
    * [ `s7access-<yyyy>-<mm>-<dd>.log`](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/c_Access_Log.html) This log is only used if dynamic media is enabled. The s7access log records each request made to Dynamic Media through `/is/image` and `/is/content`.    
    * `stderr.log` Holds error messages, again of varying levels of severity, generated during startup. By default the log level is set to `Warning` ( `WARN`)    
    * `stdout.log` Holds logging messages indicating events during startup.    
    * `upgrade.log` Provides a log of all upgrade operations that runs from the `com.day.compat.codeupgrade` and `com.adobe.cq.upgradesexecutor` packages.

* `<*cq-installation-dir*>/crx-quickstart/repository`

    * `revision.log` Revision journaling information.

>[!NOTE]
>
><p>The ImageServer and s7access logs are not included in the <b>Download Full </b>package that is generated from the <b>system/console/status-Bundlelist </b>page. For support purposes, if you have Dynamic Media issues, please also append the ImageServer and s7access logs when you contact Customer Support.&nbsp;</p>

### Activating the DEBUG Log Level

The default log level ( [Apache Sling Logging Configuration](osgi-configuration-settings.md#ApacheSlingLoggingConfiguration)) is Information, so debug messages are not logged.

To activate the debug log level for a Logger, set the property `org.apache.sling.commons.log.level` to debug in the repository. For example, on `/libs/sling/config/org.apache.sling.commons.log.LogManager` to configure the [global Apache Sling Logging](osgi-configuration-settings.md#ApacheSlingLoggingConfiguration).

>[!CAUTION]
>
><p>Do not leave the log at the debug log level longer than necessary, as it generates a lot of log entries, thus consuming resources.</p>

A line in the debug file usually starts with DEBUG, then provides the log level, the installer action and the log message. For example:

```shell
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

The log levels are as follows:

| 0 |Fatal error |The action has failed, and the installer cannot proceed. |
|---|---|---|
| 1 |Error |The action has failed. The installation proceeds, but a part of AEM WCM was not installed correctly and will not work. |
| 2 |Warning |The action has succeeded but encountered problems. AEM WCM may or may not work correctly. |
| 3 |Information |The action has succeeded. |

### Create a Custom Log File

>[!NOTE]
>
><p>When working with Adobe Experience Manager there are several methods of managing the configuration settings for such services; see <a href="/content/help/en/experience-manager/6-4/sites/deploying/using/configuring-osgi.html">Configuring OSGi</a> for more details and the recommended practices.</p>

In certain circumstances you may want to create a custom log file with a different log level. You can do this in the repository by:

1. If not already existing, create a new configuration folder ( `sling:Folder`) for your project `/apps/<*project-name*>/config`.

1. Under `/apps/<*project-name*>/config`, create a node for the new [Apache Sling Logging Logger Configuration](osgi-configuration-settings.md#ApacheSlingLoggingLoggerConfigurationFactoryConfiguration):****

    * Name: `org.apache.sling.commons.log.LogManager.factory.config-<*identifier*>` (as this is a Logger) Where `<*identifier*>` is replaced by free text that you (must) enter to identify the instance (you cannot omit this information). For example, `org.apache.sling.commons.log.LogManager.factory.config-MINE`    
    * Type: `sling:OsgiConfig`

   >[!NOTE]
   >
   ><p>Although not a technical requirement, it is advisable to make <span class="code">&lt;<i>identifier</i>&gt;</span> unique.<br> </p> 

1. Set the following properties on this node:

    * Name: `org.apache.sling.commons.log.file` Type: String Value: specify the Log File; for example, `logs/myLogFile.log`    
    * Name: `org.apache.sling.commons.log.names` Type: String[] (String + Multi) Value: specify the OSGi services for which the Logger is to log messages; for example, all of the following:

        * `org.apache.sling`        
        * `org.apache.felix`        
        * `com.day`

    * Name: `org.apache.sling.commons.log.level` Type: String Value: specify the log level required ( `debug`, `info`, `warn` or `error`); for example `debug`    
    * Configure the other parameters as required:

        * Name: `org.apache.sling.commons.log.pattern` Type: `String` Value: specify the pattern of the log message as required; for example, `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`

   >[!NOTE]
   >
   ><p><span class="code">org.apache.sling.commons.log.pattern</span> supports up to six arguments.<br> </p> <p>{0} The timestamp of type <span class="code">java.util.Date</span><br> {1} the log marker<br> {2} the name of the current thread<br> {3} the name of the logger<br> {4} the log level<br> {5} the log message<br> </p> <p>If the log call includes a <span class="code">Throwable</span> the stacktrace is appended to the message.</p> 

   >[!CAUTION]
   >
   ><p>org.apache.sling.commons.log.names must have a value.<br> </p> 

   >[!NOTE]
   >
   ><p>Log writer paths are relative to the <span class="code">crx-quickstart</span> location.</p> <p>Therefore, a log file specified as:</p> <p><span class="code">&nbsp;&nbsp;&nbsp; logs/thelog.log</span><br> </p> <p>writes to:</p> <p><span class="code">&nbsp;&nbsp;&nbsp; </span><span class="code"><span class="code"><span class="code">&lt;<i>cq-installation-dir</i>&gt;/</span></span>crx-quickstart/logs/thelog.log</span>.</p> <p>And a log file specified as:</p> <p><span class="code">&nbsp;&nbsp;&nbsp; ../logs/thelog.log</span><br> </p> <p>writes to a directory:</p> <p><span class="code">&nbsp;&nbsp;&nbsp; &lt;<i>cq-installation-dir</i>&gt;/logs/</span><br> <span class="code">&nbsp;&nbsp;&nbsp; </span>(i.e. next to&nbsp; <span class="code"><span class="code">&lt;<i>cq-installation-dir</i>&gt;/</span>crx-quickstart/</span>)</p> 

1. This step is only necessary when a new Writer is required (i.e. with a configuration that is different to the default Writer). 

   >[!CAUTION]
   >
   ><p>A new Logging Writer Configuration is only required when the existing default is not suitable.<br> </p> <p>If no explicit Writer is configured the system will automatically generate an implicit Writer based on the default.<br> </p> 
   Under `/apps/<*project-name*>/config`, create a node for the new [Apache Sling Logging Writer Configuration](osgi-configuration-settings.md#ApacheSlingLoggingWriterConfigurationFactoryConfiguration):****

    * Name: `org.apache.sling.commons.log.LogManager.factory.writer-<*identifier*>` (as this is a Writer) As with the Logger, `<*identifier*>` is replaced by free text that you (must) enter to identify the instance (you cannot omit this information). For example, `org.apache.sling.commons.log.LogManager.factory.writer-MINE`    
    * Type: `sling:OsgiConfig`

   >[!NOTE]
   >
   ><p>Although not a technical requirement, it is advisable to make <span class="code">&lt;<i>identifier</i>&gt;</span> unique.<br> </p> 
   Set the following properties on this node:

    * Name: `org.apache.sling.commons.log.file`  Type: `String` Value: specify the Log File so that it matches the file specified in the Logger;  for this example, `../logs/myLogFile.log`.    
    * Configure the other parameters as required:

        * Name: `org.apache.sling.commons.log.file.number` Type: `Long` Value: specify the number of log files you want kept; for example, `5`        
        * Name: `org.apache.sling.commons.log.file.size` Type: `String` Value: specify as required to control file rotation by size/date; for example, `'.'yyyy-MM-dd`

   >[!NOTE]
   >
   ><p><span class="code">org.apache.sling.commons.log.file.size</span> controls the rotation of the log file by setting either:</p> <ul> <li>a maximum file size</li> <li>a time/date schedule <br> </li> </ul> <p>to indicate when a new file will be created (and the existing file renamed according to the name pattern).<br> </p> <ul> <li>A size limit can be specified with a number. If no size indicator is given, then this is taken as the number of bytes, or you can add one of the size indicators - <span class="code">KB</span>, <span class="code">MB</span>, or <span class="code">GB</span> (case is ignored).</li> <li>A time/date schedule can be specified as a <span class="code">java.util.SimpleDateFormat</span> pattern. This defines the time period after which the file will be rotated; also the suffix appended to the rotated file (for identification).<br> The default is '.'yyyy-MM-dd (for daily log rotation). <br> So for example, at midnight of January 20th 2010 (or when the first log message after this occurs to be precise), ../logs/error.log will be renamed to ../logs/error.log.2010-01-20. Logging for the 21st of January will be output to (a new and empty) ../logs/error.log until it is rolled over at the next change of day.<br> <table cellpadding="2" border="1"><tbody> <tr> <td><span class="code">'.'yyyy-MM</span></td> <td>Rotation at the beginning of each month</td> </tr> <tr> <td><span class="code">'.'yyyy-ww</span></td> <td>Rotation&nbsp;at the first day of each week (depends on the locale).</td> </tr> <tr> <td><span class="code">'.'yyyy-MM-dd</span></td> <td>Rotation&nbsp;at midnight each day.</td> </tr> <tr> <td><span class="code">'.'yyyy-MM-dd-a</span></td> <td>Rotation&nbsp;at midnight and midday of each day.</td> </tr> <tr> <td><span class="code">'.'yyyy-MM-dd-HH</span></td> <td>Rotation&nbsp;at the top of every hour.</td> </tr> <tr> <td><span class="code">'.'yyyy-MM-dd-HH-mm</span></td> <td>Rotation&nbsp;at the beginning of every minute.</td> </tr> </tbody> </table> Note: When specifying a time/date:<br> &nbsp;&nbsp;&nbsp; 1. You should &quot;escape&quot; literal text within a pair of single quotes (' '); <br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; this is to avoid certain characters being interpreted as pattern letters.<br> &nbsp;&nbsp;&nbsp; 2. Only use characters allowed for a valid file name anywhere in the option.</li> </ul> 

1. Read your new log file with your chosen tool.

   The log file created by this example will be `../crx-quickstart/logs/myLogFile.log`.

The Felix Console also provides information about Sling Log Support at `../system/console/slinglog`; for example `http://localhost:4502/system/console/slinglog`.

### Finding the Audit Records

Audit records are held to provide a record of who did what and when. Different audit records are generated for both AEM WCM and OSGi events.

#### AEM WCM Audit records shown when Page Authoring

1. Open a page.

1. From the sidekick you can select the tab with the lock icon, then double-click on **Audit Log...**

1. A new window will open showing the list of audit records for the current page.
   ![](assets/screen_shot_2012-02-02at43601pm.png)
1. Click **OK** when you want to close the window.

#### AEM WCM Auditing records within the repository

Within the `/var/audit` folder, audit records are held according to the resource. You can drill down until you can see the individual records and the information they contain.

These entries hold the same information as shown when editing a page.

#### OSGi Audit records from the Web Console

OSGi events also generate audit records which can be seen from the **Configuration Status** tab -&gt; **Log Files **tab in the Adobe CQ Web Console: 
![](assets/screen_shot_2012-02-13at50346pm.png) 

---

## Monitoring Your Replication Agents

You can monitor your [replication queues](replication.md) to detect when a queue is either down or blocked - which might in turn indicate a problem with a publishing instance or external system:

* are all required queues enabled?
* are any disabled queues still required?
* all `enabled` queues should have the status `idle` or `active`, which indicate normal operation; no queues should be `blocked`, which is often a sign of problems on the receivers side.
* if the size of the queue grows over time this can indicate a blocked queue.

To monitor a replication agent:

1. Access the **Tools** tab in AEM.

1. Click **Replication**.

1. Double-click the link to agents for the appropriate environment (either the left or the right pane); for example **Agents on author**.

   The resulting window shows an overview of all your replication agents for the author environment, including their target and status.

1. Click the appropriate agent name (which is a link) to show detailed information on that agent:
   ![](assets/chlimage_1.jpeg)Here you can:

    * See whether the agent is enabled.    
    * See the target of any replications.    
    * See whether the replication queue is currently active (enabled).    
    * See whether there are any items in the queue.    
    * **Refresh** or **Clear** to update the display of queue entries; this helps you see items enter and leave the queue.    
    * **View Log** to access the log of any actions by the replication agent.    
    * **Test Connection** to the target instance.    
    * **Force Retry** on any queue items if required.

   >[!CAUTION]
   >
   ><p>Do not use the &quot;Test Connection&quot; link for the Reverse Replication Outbox on a publish instance.</p> <p>If a replication test is performed for an Outbox queue, any items that are older than the test replication will be re-processed with every reverse replication.<br> </p> <p>If such items already exist in a queue, they can be found with the following XPath JCR query and should be removed.<br> </p> <p><span class="code">/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']</span>&nbsp;</p>

Again you can develop a solution to detect all replication agents (located under `/etc/replication/author` or `/etc/replication/publish`), then check the status of the agent ( `enabled`, `disabled`) and the underlying queue ( `active`, `idle`, `blocked`).

---

## Monitoring Performance

[Performance Optimization](configuring-performance.md) is an interactive process which receives focus during development. After deployment it is usually reviewed after specific intervals or events.

Methods used while collecting information for optimization can also be used for ongoing monitoring. 

>[!NOTE]
>
><p>Specific <a href="/content/help/en/experience-manager/6-4/sites/deploying/using/configuring-performance.html#ConfiguringforPerformance">configurations available to improve performance</a> can also be checked.<br> </p>

The following lists common performance issues which occur, together with proposals on how to spot and counteract them.

| Area |Symptom(s) |To increase capacity... |To reduce volume... |
|---|---|---|---|
| Client |High client CPU usage. |Install a client CPU with higher performance. |Simplify (HTML) layout. |
|   |Low server CPU usage. |Upgrade to a faster browser. |Improve client-side cache. |
|   |Some clients fast, some slow. |  |  |
| Server |  |  |  |
| Network |CPU usage low on both servers and clients. |Remove any network bottlenecks. |Improve/optimize the configuration of the client cache. |
|   |Browsing locally on the server is (comparatively) fast. |Increase network bandwidth. |Reduce the "weight" of your web pages (e.g. less images, optimized HTML). |
| Web-server |CPU usage on the web-server is high. |Cluster your web-servers. |Reduce the hits per page (visit). |
|   |  |Use a hardware load-balancer. |  |
| Application |Server CPU usage is high. |Cluster your CQ5 instances. |Search for, and eliminate, CPU and memory hogs (use code review, timing output, etc). |
|   |High memory consumption. |  |Improve caching on all levels. |
|   |Low response times. |  |Optimize templates and components (e.g. structure, logic). |
| Repository |  |  |  |
| Cache |  |  |  |

Performance issues may stem from a number of causes that have nothing to do with your website, including temporary slowdowns in connection speed, CPU load, and many more.

It may also impact either all your visitors, or only a subset of them.

All this information needs to be obtained, sorted and analyzed before you can either optimize the general performance or solve specific issues.

* Before you experience a performance issue:

    * collect as much information as possible to build up a good working knowledge of the system under normal circumstances

* When you experience a performance issue:

    * try to replicate it with one (or preferably more) standard web-browsers, on a different client that you know has good general performance and/or on the server itself (if possible)    
    * check whether anything (related to the system) has changed within an appropriate time-space, and if any of these changes could have impacted the performance    
    * ask questions such as:

        * does the issue only occur at specific times?        
        * does the issue only occur on specific pages?        
        * are other requests impacted?

    * collect as much information as possible to compare with your knowledge of the system under normal circumstances:

### Tools for Monitoring and Analyzing Performance

The following gives a short overview of some of the tools available for monitoring and analyzing performance.

Some of these will be dependent on your operating system.

<table border="1" cellpadding="1" cellspacing="0" width="100%"> 
 <tbody> 
  <tr> 
   <td>Tool</td> 
   <td>Used to analyze...</td> 
   <td>Usage / More information...</td> 
  </tr> 
  <tr> 
   <td>request.log</td> 
   <td>Response times and concurrency.</td> 
   <td><a href="#Interpretingtherequestlog">Interpreting the request.log</a>.</td> 
  </tr> 
  <tr> 
   <td>truss/strace</td> 
   <td>Page Loads</td> 
   <td><p>Unix/Linux commands to trace system calls and signals. Increase the log level to <span class="code">INFO</span>.</p> <p>Analyze the number of page loads per request, which pages, etc.</p> </td> 
  </tr> 
  <tr> 
   <td>Thread dumps</td> 
   <td>Observe JVM threads. Identify contentions, locks and long-runners.</td> 
   <td><p>Dependent on the operating system:<br /> - Unix/Linux: <span class="code">kill -QUIT &lt;<i>pid</i>&gt;</span><br /> - Windows (console mode): Ctrl-Break<br /> </p> <p>Analysis tools are also available, such as <a href="http://java.net/projects/tda/">TDA</a>.<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>Heap Dumps</td> 
   <td>Out of Memory issues that cause slow performance.</td> 
   <td><p>Add the:<br /> <span class="code">-XX:+HeapDumpOnOutOfMemoryError</span><br /> option to the java call to CQ.</p> <p>See the <a href="http://java.sun.com/javase/6/webnotes/trouble/TSG-VM/html/clopts.html#gbzrr">Troubleshooting Guide for Java SE 6 with HotSpot VM</a>.</p> </td> 
  </tr> 
  <tr> 
   <td>System calls</td> 
   <td>Identify timing issues.</td> 
   <td><p>Calls to <span class="code">System.currentTimeMillis()</span> or <span class="code">com.day.util</span>.Timing are used to generate timestamps from your code, or via <a href="#HTMLComments">HTML-comments</a>.</p> <p><strong>Note:</strong> These should be implemented so that they can be activated / deactivated as required; when a system is running smoothly the overhead of collecting statistics will not be needed.</p> </td> 
  </tr> 
  <tr> 
   <td>Apache Bench</td> 
   <td>Identify memory leaks, selectively analyze response time.</td> 
   <td><p>basic usage is:</p> <p><span class="code">ab -k -n &lt;<i>requests</i>&gt; -c &lt;<i>concurrency</i>&gt; &lt;<i>url</i>&gt;</span></p> <p>See <a href="#ApacheBench">Apache Bench</a> and the <a href="http://httpd.apache.org/docs/2.2/programs/ab.html">ab man page</a> for full details.</p> </td> 
  </tr> 
  <tr> 
   <td>Search Analysis</td> 
   <td> </td> 
   <td>Execute search queries offline, identify response time of query, test and confirm result set.<br /> </td> 
  </tr> 
  <tr> 
   <td>JMeter</td> 
   <td>Load and functional tests.</td> 
   <td><a href="http://jakarta.apache.org/jmeter/">http://jakarta.apache.org/jmeter/</a></td> 
  </tr> 
  <tr> 
   <td>JProfiler</td> 
   <td>In-depth CPU and memory profiling.</td> 
   <td><a href="http://www.ej-technologies.com/">http://www.ej-technologies.com/</a></td> 
  </tr> 
  <tr> 
   <td>JConsole</td> 
   <td>Observe JVM metrics and threads.</td> 
   <td><p>Usage: jconsole</p> <p>See <a href="http://java.sun.com/developer/technicalArticles/J2SE/jconsole.html">jconsole</a> and <a href="#MonitoringPerformanceusingJConsole">Monitoring Performance using JConsole</a>.</p> <p><strong>Note:</strong> With JDK 1.6, JConsole is extensible with plug-ins; for example, Top or TDA (Thread Dump Analyzer).</p> </td> 
  </tr> 
  <tr> 
   <td>Java VisualVM</td> 
   <td>Observe JVM metrics, threads, memory and profiling.</td> 
   <td><p>Usage: jvisualvm or visualvm<br /> </p> <p>See <a href="http://java.sun.com/javase/6/docs/technotes/tools/share/jvisualvm.html">jvisualvm</a>, <a href="https://visualvm.dev.java.net/">visualvm</a> and <a href="#MonitoringPerformanceusingJVisualVM">Monitoring Performance using (J)VisualVM</a>.</p> <p><strong>Note:</strong> With JDK 1.6, VisualVM is extensible with plug-ins.</p> </td> 
  </tr> 
  <tr> 
   <td>truss/strace, lsof</td> 
   <td>In depth kernel call and process analysis (Unix).</td> 
   <td>Unix/Linux commands.</td> 
  </tr> 
  <tr> 
   <td>Timing Statistics</td> 
   <td>See timing statistics for page rendering.</td> 
   <td><p>To see timing statistics for page rendering you can use <strong>Ctrl-Shift-U</strong> together with <span class="code">?debugClientLibs=true</span> set in the URL.</p> </td> 
  </tr> 
  <tr> 
   <td>CPU and memory profiling tool<br /> </td> 
   <td><a href="#Interpretingtherequestlog">Used when analyzing slow requests during development</a>.</td> 
   <td>For example, <a href="http://www.yourkit.com/">YourKit</a>.</td> 
  </tr> 
  <tr> 
   <td><a href="#InformationCollection">Information Collection</a></td> 
   <td>The ongoing state of your installation.</td> 
   <td>Knowing as much as possible about your installation can also help you track down what might have caused a change in performance, and whether these changes are justified. These metrics need to be collected at regular intervals so you can easily see significant changes.</td> 
  </tr> 
 </tbody> 
</table>

### Interpreting the request.log

This file registers basic information about every request made to CQ. From this valuable conclusions can be extracted.

The `request.log` offers a built-in way to get a look at how long requests take. For development purposes it is useful to `tail -f` the `request.log` and watch for slow response times. To analyze a bigger `request.log` we recommend the [use of `rlog.jar` which allows you to sort and filter for response times](#Usingrlogjartofindrequestswithlongdurationtimes).

We recommend isolating the "slow" pages from the `request.log`, then individually tuning them for a better performance. This is usually done by including performance metrics per component or using a performance profiling tool such as ` [yourkit](http://www.yourkit.com/)`.

#### Monitoring traffic on your website

The request log registers each request made, together with the response made:

```xml
09:43:41 [66] -> GET /author/y.html HTTP/1.1
09:43:41 [66] <- 200 text/html 797ms
```

By totaling all the GET entries within a specific periods (e.g. over various 24 hour periods) you can make statements about the average traffic on your website.

#### Monitoring response times with the CQ request.log

A good starting point for performance analysis is the request log:

`<*cq-installation-dir*>/crx-quickstart/logs/request.log`

The log looks as follows (the lines are shortened for simplicity):

```xml
31/Mar/2009:11:32:57 +0200 [379] -> GET /path/x HTTP/1.1 
31/Mar/2009:11:32:57 +0200 [379] <- 200 text/html 33ms 
31/Mar/2009:11:33:17 +0200 [380] -> GET /path/y HTTP/1.1 
31/Mar/2009:11:33:17 +0200 [380] <- 200 application/json 39ms
```

This log has one line per request or response:

* The date at which each request or response was made.
* The number of the request, in square brackets. This number matches for the request and the response.
* An arrow indicating whether this is a request (arrow pointing to the right) or a response (arrow to the left).
* For requests, the line contains:

    * the method (typically, GET, HEAD or POST)    
    * the requested page    
    * the protocol

* For responses, the line contains:

    * the status code (200 means “success”, 404 means “page not found”    
    * the MIME type    
    * the response time

Using small scripts, you can extract the required information from the log file and assemble the statistics you want. From these, you can see which pages or types of pages are slow, and if the overall performance is satisfactory.

#### Monitoring search response times with the CQ5 request.log

Search requests are also registered in the log file:

```xml
31/Mar/2009:11:35:34 +0200 [338] -> GET /author/playground/en/tools/search.html?query=dilbert&size=5&dispenc=utf-8 HTTP/1.1
31/Mar/2009:11:35:34 +0200 [338] <- 200 text/html 1562ms
```

So, as above, you can use scripts to extract the relevant information and build up statistics.

However, once you have determined the response time, you may need to analyze why the request is taking the time it does, and what can be done to improve the response.

#### Monitoring the number and impact of concurrent users

Again the `request.log` can be used to monitor concurrency and the system's reaction to it.

Tests must be made to determine how many concurrent users the system can handle before a negative impact is seen. Again scripts can be used to extract results from the log file:

* monitor how many requests are made within a specific time span e.g. one minute
* test the effects of a specific number of users all making the same requests at (as close as possible) the same time; e.g. 30 users clicking **Save** at the same time.

```xml
31/Mar/2009:11:45:29 +0200 [333] -> GET /author/libs/Personalize/content/statics.close.gif HTTP/1.1
31/Mar/2009:11:45:29 +0200 [334] -> GET /author/libs/Personalize/content/statics.detach.gif HTTP/1.1
31/Mar/2009:11:45:30 +0200 [335] -> GET /author/libs/CFC/content/imgs/logo.rZMNURccynWcTpCxyuBNiTCoiBMmw000.default.gif HTTP/1.1
31/Mar/2009:11:45:32 +0200 [335] <- 304 text/html 0ms
31/Mar/2009:11:45:33 +0200 [334] <- 200 image/gif 31ms
31/Mar/2009:11:45:38 +0200 [333] <- 200 image/gif 31ms
31/Mar/2009:11:45:42 +0200 [336] -> GET /author/libs/CFC/content/imgs/logo.rZMNURccynWcTZRXunQbbQtvuuCMbRRBuWXz0000.default.gif HTTP/1.1
31/Mar/2009:11:45:43 +0200 [337] -> GET /author/titlebar_bg.gif HTTP/1.1
31/Mar/2009:11:45:43 +0200 [336] <- 304 text/html 0ms
31/Mar/2009:11:45:44 +0200 [337] <- 304 text/html 0ms
```

### Using rlog.jar to find requests with long duration times

CQ includes various helper tools located in: `<*cq-installation-dir*>/crx-quickstart/opt/helpers`

One of these, `rlog.jar`, can be used to quickly sort `request.log` so that requests are displayed by duration, from longest to shortest time.

The following command shows the possible arguments:

```shell
$java -jar rlog.jar 
Request Log Analyzer Version 21584 Copyright 2005 Day Management AG 
Usage: 
  java -jar rlog.jar [options] <filename> 
Options: 
  -h               Prints this usage. 
  -n <maxResults>  Limits output to <maxResults> lines. 
  -m <maxRequests> Limits input to <maxRequest> requests. 
  -xdev            Exclude POST request to CRXDE.
```

For example, you can run it specifying `request.log` file as a parameter and show the 10 first requests that have the longest duration:

```shell
$ java -jar ../opt/helpers/rlog.jar -n 10 request.log 
*Info * Parsed 464 requests. 
*Info * Time for parsing: 22ms 
*Info * Time for sorting: 2ms 
*Info * Total Memory: 1mb 
*Info * Free Memory: 1mb 
*Info * Used Memory: 0mb 
------------------------------------------------------ 
     18051ms 31/Mar/2009:11:15:34 +0200 200 GET /content/geometrixx/en/company.html text/ html 
      2198ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/cq/widgets.js application/x-javascript 
      1981ms 31/Mar/2009:11:15:11 +0200 200 GET /libs/wcm/content/welcome.html text/html 
      1973ms 31/Mar/2009:11:15:52 +0200 200 GET /content/campaigns/geometrixx.teasers..html text/html 
      1883ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/security/cq-security.js application/x-javascript 
      1876ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/tagging/widgets.js application/x-javascript
      1869ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/tagging/widgets/themes/default.js application/x-javascript 
      1729ms 30/Mar/2009:16:45:56 +0200 200 GET /libs/wcm/content/welcome.html text/html; charset=utf-8 
      1510ms 31/Mar/2009:11:15:34 +0200 200 GET /bin/wcm/contentfinder/asset/view.json/ content/dam?_dc=1238490934657&query=&mimeType=image&_charset_=utf-8 application/json 
      1462ms 30/Mar/2009:17:23:08 +0200 200 GET /libs/wcm/content/welcome.html text/html; charset=utf-8 
```

You may need to concatenate the individual `request.log` files if you need to do this operation on a large data sample.

### Apache Bench

To minimize the impact of special cases (such as garbage collection, etc), it is recommended to use a tool such as `apachebench` (see for example, [ab](http://httpd.apache.org/docs/2.2/programs/ab.html) for further documentation) to help identify memory leaks and selectively analyze response time.

Apache Bench can be used in the following way:

```shell
$ ab -c 5 -k -n 1000 "http://localhost:4503/content/geometrixx/en/company.html"
This is ApacheBench, Version 2.3 <$Revision: 655654 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking localhost (be patient)
Completed 100 requests
Completed 200 requests
Completed 300 requests
Completed 400 requests
Completed 500 requests
Completed 600 requests
Completed 700 requests
Completed 800 requests
Completed 900 requests
Completed 1000 requests
Finished 1000 requests

Server Software: Day-Servlet-Engine/4.1.52
Server Hostname: localhost
Server Port: 4503

Document Path: /content/geometrixx/en/company.html
Document Length: 24127 bytes

Concurrency Level: 5
Time taken for tests: 69.766 seconds
Complete requests: 1000
Failed requests: 998
(Connect: 0, Receive: 0, Length: 998, Exceptions: 0)
Write errors: 0
Keep-Alive requests: 0
Total transferred: 24160923 bytes
HTML transferred: 24010923 bytes
Requests per second: 14.33 /sec (mean)
Time per request: 348.828 [ms] (mean)
Time per request: 69.766 [ms] (mean, across all concurrent requests)
Transfer rate: 338.20 [Kbytes/sec] received

Connection Times (ms)
min mean[+/-sd] median max
Connect: 0 1 3.9 0 58
Processing: 138 347 568.5 282 8106
Waiting: 137 344 568.1 281 8106
Total: 139 348 568.4 283 8106

Percentage of the requests served within a certain time (ms)
50% 283
66% 323
75% 356
80% 374
90% 439
95% 512
98% 1047
99% 1132
100% 8106 (longest request)
```

The numbers above are taken from a standard MAcBook Pro laptop (mid 2010) accessing the geometrixx company page, as included in a default CQ 5.6.1 installation. The page is very simple, but not optimized for performance.

`apachebench` also displays the time per request as the mean, across all concurrent requests; see `Time per request: 54.595 [ms]` (mean, across all concurrent requests). You can change the value of the concurrency parameter `-c` (number of multiple requests to perform at a time) to see any effects.

### Request Counters

Information about request traffic (number of requests during a specific time period) gives you an indication of the load on your instance. This information can be extracted from [request.log](#Interpretingtherequestlog), though using counters will automate data collection to let you see:

* significant differences in activity (ie differentiate between "many requests" and "low activity"
* when an instance is not being used
* any restarts (counters are reset to 0)

To automate information collection you can also install a RequestFilter to increment a counter on every request. Multiple counters can be used for different time periods.

The information gathered can be used to indicate:

* significant changes in activity
* a redundant instance
* any restarts (counter reset to 0)

### HTML Comments

It is recommended that every project includes `html comments` for server performance. Many good public examples can be found; select a page, open the page source for viewing and scroll to the bottom, code such as the following can be seen:

```xml
</body>
 </html>
        <!--
        Page took 58 milliseconds to be rendered by server
         -->

```

### Monitoring Performance using JConsole

The tool command `jconsole` is available with the JDK.

1. Start your CQ5 instance.

1. Run `jconsole.`

1. Select your CQ instance and **Connect**. 

1. From within the `Local` application, double-click `com.day.crx.quickstart.Main`; the Overview will be shown as default: 
   ![](assets/chlimage_1.png)After this you can select other options.

### Monitoring Performance using (J)VisualVM

Since JDK 1.6, the tool command `jvisualvm` is available. After you have installed JDK 1.6 you can:

1. Start your CQ5 instance.

   >[!NOTE]
   >
   ><p>If using Java 5 you can add the <span class="code">-Dcom.sun.management.jmxremote</span> argument to the java command line that starts your JVM. JMX is enabled per default with Java 6.<br> </p> 

1. Run either:

    * `jvisualvm`: in the JDK 1.6 bin folder (tested version)    
    * `visualvm`: can be downloaded from [VisualVM](https://visualvm.dev.java.net/) (bleeding edge version)

1. From within the `Local` application, double-click `com.day.crx.quickstart.Main`; the Overview will be shown as default: 
   ![](assets/chlimage_1.png)After this you can select other options, including Monitor: 
   ![](assets/chlimage_1.png)

You can use this tool to generate thread dumps and memory head dumps. This information is often requested by the technical support team.

### Information Collection

Knowing as much as possible about your installation can help you track down what might have caused a change in performance, and whether these changes are justified. These metrics need to be collected at regular intervals so you can easily see significant changes.

The following information can be useful:

* [How many authors are working with the system?](#Howmanyauthorsareworkingwiththesystem)
* [What is the average number of page activations per day?](#Whatistheaveragenumberofpageactivationsperday)
* [How many pages do you currently maintain on this system?](#Howmanypagesdoyoucurrentlymaintainonthissystem)
* [If you use MSM, what is the average number of rollouts per month?](#IfyouuseMSMwhatistheaveragenumberofrolloutspermonth)
* [What is the average number of Live Copies per month?](#WhatistheaveragenumberofLiveCopiespermonth)
* [If you use CQ DAM, how many assets do you currently maintain in CQ DAM?](#IfyouuseCQDAMhowmanyassetsdoyoucurrentlymaintaininCQDAM)
* [What is the average size of the assets?](#Whatistheaveragesizeoftheassets)
* [How many templates are currently used?](#Howmanytemplatesarecurrentlyused)
* [How many components are currently used?](#Howmanycomponentsarecurrentlyused)
* [How many requests per hour do you have on the author system at peak time?](#Howmanyrequestsperhourdoyouhaveontheauthorsystematpeaktime)
* [How many requests per hour do you have on the publish system at peak time?](#Howmanyrequestsperhourdoyouhaveonthepublishsystematpeaktime)

Knowing as much as possible about your installation can help you track down what might have caused a change in performance, and whether these changes are justified. These metrics need to be collected at regular intervals so you can easily see significant changes.

The following information can be useful:

* [How many authors are working with the system?](#Howmanyauthorsareworkingwiththesystem)
* How many authoring servers do you use?
* What hardware do you use for the author server(s)?
* [What is the average number of page activations per day?](#Whatistheaveragenumberofpageactivationsperday)
* [How many pages do you currently maintain on this system?](#Howmanypagesdoyoucurrentlymaintainonthissystem)
* [If you use MSM, what is the average number of rollouts per month?](#IfyouuseMSMwhatistheaveragenumberofrolloutspermonth)
* [What is the average number of Live Copies per month?](#WhatistheaveragenumberofLiveCopiespermonth)
* [If you use CQ DAM, how many assets do you currently maintain in CQ DAM?](#IfyouuseCQDAMhowmanyassetsdoyoucurrentlymaintaininCQDAM)
* [What is the average size of the assets?](#Whatistheaveragesizeoftheassets)
* How many publish servers do you use?
* What hardware do you use for the publish server(s)?
* [How many templates are currently used?](#Howmanytemplatesarecurrentlyused)
* [How many components are currently used?](#Howmanycomponentsarecurrentlyused)
* [How many requests per hour do you have on the author system at peak time?](#Howmanyrequestsperhourdoyouhaveontheauthorsystematpeaktime)
* [How many requests per hour do you have on the publish system at peak time?](#Howmanyrequestsperhourdoyouhaveonthepublishsystematpeaktime)

#### How many authors are working with the system?

To see the number of authors that have used the system since installation use the command line:

```shell
cd <cq-installation-dir>/crx-quickstart/logs
cut -d " " -f 3 access.log | sort -u | wc -l
```

To see the number of authors working on a given date:

```shell
grep "<date>" access.log | cut -d " " -f 3 | sort -u | wc -l
```

#### What is the average number of page activations per day?

To see the total number of page activations since server installation use a repository query; via CRXDE - Tools - Query:

* **Type** `XPath`
* **Path** `/`
* **Query** `//element(*, cq:AuditEvent)[@cq:type='Activate']`

Then calculate the number of days that have elapsed since installation to calculate the average.

#### How many pages do you currently maintain on this system?

To see the number of pages currently on the server use a repository query; via CRXDE - Tools - Query:

* **Type** `XPath`
* **Path** `/`
* **Query** `//element(*, cq:Page)`

#### If you use MSM, what is the average number of rollouts per month?

To determine the total number of rollouts since installation use a repository query; via CRXDE - Tools - Query:

* **Type** `XPath`
* **Path** `/`
* **Query** `//element(*, cq:AuditEvent)[@cq:type='PageRolledOut']`

Calculate the number of months that have elapsed since installation to calculate the average.

#### What is the average number of Live Copies per month?

To determine the total number of Live Copies made since installation use a repository query; via CRXDE - Tools - Query:

* **Type** `XPath`
* **Path** `/`
* **Query** `//element(*, cq:LiveSyncConfig)`

Again use the number of months that have elapsed since installation to calculate the average.

#### If you use CQ DAM, how many assets do you currently maintain in CQ DAM?

To see how many DAM assets you currently maintain, use a repository query; via CRXDE - Tools - Query:

* **Type** `XPath`
* **Path** `/`
* **Query** `/jcr:root/content/dam//element(*, dam:Asset)`

#### What is the average size of the assets?

To determine the total size of the `/var/dam` folder:

1. Use WebDAV to map the CQ repository to the local file system. 

1. Use the command line:

   ```shell
   cd /Volumes/localhost/var
   du -sh dam/
   ```

   To get the average size, divide the global size by the total number of assets in `/var/dam` (obtained above).

#### How many templates are currently used?

To see the number of templates currently on the server use a repository query; via CRXDE - Tools - Query:

* **Type** `XPath`
* **Path** `/`
* **Query** `//element(*, cq:Template)`

#### How many components are currently used?

To see the number of components currently on the server use a repository query; via CRXDE - Tools - Query:

* **Type** `XPath`
* **Path** `/`
* **Query** `//element(*, cq:Component)`

#### How many requests per hour do you have on the author system at peak time?

To determine the requests per hour you have on the author system at peak time:

1. To determine the total number of requests since installation use the command line:

   ```shell
   cd <cq-installation-dir>/crx-quickstart/logs
   grep -R "\->" request.log | wc -l
   ```

1. To determine the start and end dates:

   ```shell
   vim request.log
   G / 1G: for the last/first lines
   ```

   Use these values to calculate the number of hours that have elapsed since installation, then the average number of requests per hour.

#### How many requests per hour do you have on the publish system at peak time?

Repeat the above procedure on your publish instance.

---

## Analyzing Specific Scenarios

The following is a list of suggestions on what to check if you start experiencing certain CQ performance problems. The list is not (unfortunately) fully comprehensive. 

>[!NOTE]
>
><p>See also the following articles for more information:</p> <ul> <li><a href="https://helpx.adobe.com/experience-manager/kb/TakeThreadDump.html">Thread dumps</a></li> <li><a href="/content/help/en/experience-manager/kb/AnalyzeMemoryProblems.html">Analyze memory problems</a></li> <li><a href="https://helpx.adobe.com/experience-manager/kb/AnalyzeUsingBuiltInProfiler.html">Analyze using built-in profiler</a></li> <li><a href="/content/help/en/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html">Analyze slow and blocked processes</a></li> </ul>

### CPU at 100%

If the CPU of your system is constantly running at 100% then see:

* The Knowledge Base:

    * [Analyze Slow and Blocked Processes](/content/help/en/experience-manager/kb/AnalyzeSlowAndBlockedProcesses)

### Out of Memory

Although such errors should be detected during Development and Testing, certain scenarios can slip through.

If your system is running out of memory this can be seen in various ways, including performance degradation and error messages including the subtext:

`java.lang.OutOfMemoryError`

In these cases check:

* the JVM settings used to [start AEM](deploy.md#GettingStarted)
* The Knowledge Base:

    * [Analyze Memory Problems](/content/help/en/experience-manager/kb/AnalyzeMemoryProblems)

### Disk I/O

If your system is either running out of diskspace, or you notice disk thrashing starting see:

* Whether you have disabled collection of debug information; this can be configured in various locations, including:

    * [Apache Sling JSP Script Handler](osgi-configuration-settings.md#ApacheSlingJSPScriptHandler)    
    * [Apache Sling Java Script Handler](osgi-configuration-settings.md#ApacheSlingJavaScriptHandler)    
    * [Apache Sling Logging Configuration](osgi-configuration-settings.md#ApacheSlingLoggingConfiguration)    
    * [CQ HTML Library Manager](osgi-configuration-settings.md#DayCQHTMLLibraryManager)    
    * [CQ WCM Debug Filter](osgi-configuration-settings.md#DayCQWCMDebugFilter)    
    * [Loggers](monitoring-and-maintaining.md#ActivatingtheDEBUGLogLevel) [](configuring.md#LoggersandWritersforIndividualServices)

* Whether and how you have configured [Version Purging](version-purging.md)
* The Knowledge Base:

    * [Too Many Open Files](/content/help/en/experience-manager/kb/TooManyOpenFiles)    
    * [Journal consumes too much diskspace](/content/help/en/experience-manager/kb/JournalTooMuchDiskSpace)

### Regular Performance Degradation

If you see the performance of your instance deteriorating after each reboot (sometimes a week or more later), then the following can be checked:

* [Out of Memory](#OutofMemory)
* The Knowledge Base:

    * [Unclosed Sessions](/content/help/en/experience-manager/kb/AnalyzeUnclosedSessions)

### JVM Tuning

The Java Virtual Machine (JVM) has significantly improved in respect to tuning (especially since Java 7). Because of this, specifying a reasonable fixed JVM size and using the defaults will often be suitable.

If the default settings are not suitable, then it is important to establish a method to monitor and assess GC performance before attempting to tune the JVM; this can involve monitoring factors including, heap size, algorithm and other aspects.

Some common choices are:

* VerboseGC: `-verbose:gc \ -Xloggc:$LOGS/verbosegc.log \ -XX:+PrintGCDetails \ -XX:+PrintGCDateStamps`

The resulting log can be ingested by a GC visualizer such as:

` [http://www.ibm.com/developerworks/library/j-ibmtools2/](http://www.ibm.com/developerworks/library/j-ibmtools2/)`

Or JConsole:

* These settings are for a "wide open" JMX connection: `-Dcom.sun.management.jmxremote \ -Dcom.sun.management.jmxremote.port=8889 \ -Dcom.sun.management.jmxremote.authenticate=false \ -Dcom.sun.management.jmxremote.ssl=false`
* Then connect to the JVM with the JConsole; see: ` [http://docs.oracle.com/javase/6/docs/technotes/guides/management/jconsole.html](http://docs.oracle.com/javase/6/docs/technotes/guides/management/jconsole.html)`

This will help you see how much memory is being used, what GC algorithms are being used, how long they take to run, and what effect this has on your application performance. Without this, tuning is just "randomly twiddling knobs".

>[!NOTE]
>
><p>For Oracle's VM there is also information at:</p> <p><a href="http://docs.oracle.com/javase/7/docs/technotes/guides/vm/server-class.html">http://docs.oracle.com/javase/7/docs/technotes/guides/vm/server-class.html</a></p> 