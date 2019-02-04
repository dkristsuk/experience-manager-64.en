---
title: Backup and Restore Service APIQuick Starts
seo-title: Backup and Restore Service APIQuick Starts
description: null
seo-description: null
uuid: 493b230d-cbd1-4bf6-91d2-f5bbd64593b1
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
discoiquuid: e7fc5096-bd62-4045-90ba-7fdcd304b4a0
index: y
internal: n
snippet: y
---

# Backup and Restore Service APIQuick Starts{#backup-and-restore-service-apiquick-starts}

Java API Quick Start(SOAP) are available for the Backup and Restore Service API.

[Quick Start: Entering backup mode using the Java API(SOAP)](backup-restore-service-api-quick#quick_start_soap_mode_entering_backup_mode_using_the_java_api)

[Quick Start: Leaving backup mode using the Java API(SOAP)](backup-restore-service-api-quick#quick_start_soap_mode_leaving_backup_mode_using_the_java_api)

AEM Forms operations can be performed using the AEM Forms strongly-typed API and the connection mode should be set to SOAP.

* ***Note**: Quick Starts located in Programming with AEM Forms are based on the Forms operating system. However, if you are using another operating system, such as UNIX, replace Windows-specific paths with paths that are supported by the applicable operating system. Likewise, if you are using another J2EE application server, ensure that you specify valid connection properties. (See [Setting connection properties](/programming-with-aem-forms/invoking-aem-forms-using-java#setting_connection_properties).*

## Quick Start (SOAP mode): Entering backup mode using the Java API {#quick-start-soap-mode-entering-backup-mode-using-the-java-api}

The following Java code example enters into backup mode with a unique label for two hours. After the backup time expires or if backup mode is explicitly exited, the forms server returns to purging files from the Global Document Storage. (See [Entering Backup Mode on the forms server](/programming-with-aem-forms/preparing-aem-forms-backup#entering_backup_mode_on_the_forms_server).)

```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-backup-restore-client-sdk.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
    * 4. activation.jar (required for SOAP mode) 
    * 5. axis.jar (required for SOAP mode) 
    * 6. commons-codec-1.3.jar (required for SOAP mode) 
    * 7. commons-collections-3.2.jar  (required for SOAP mode) 
    * 8. commons-discovery.jar (required for SOAP mode) 
    * 9. commons-logging.jar (required for SOAP mode) 
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
    * 12. jaxrpc.jar (required for SOAP mode) 
    * 13. log4j.jar (required for SOAP mode) 
    * 14. mail.jar (required for SOAP mode) 
    * 15. saaj.jar (required for SOAP mode) 
    * 16. wsdl4j.jar (required for SOAP mode) 
    * 17. xalan.jar (required for SOAP mode) 
    * 18. xbean.jar (required for SOAP mode) 
    * 19. xercesImpl.jar (required for SOAP mode) 
     * 
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to  
     * your local development environment and then include the 3 JBoss JAR files in your class path 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * 
     * <install directory>/jboss/bin/client 
     * 
     * If you want to invoke a remote forms server instance and there is a 
     * firewall between the client application and the server, then it is  
     * recommended that you use the SOAP mode. When using the SOAP mode,  
     * you have to include additional JAR files located in the following  
     * path 
     * <install directory>/sdk/client-libs/thirdparty 
     * 
     * For information about the SOAP  
     * mode and the additional JAR files that need to be included,  
     * see "Setting connection properties" in Programming  
     * with AEM Forms 
     * 
     * For complete details about the location of the AEM Forms JAR files,  
     * see "Including AEM Forms Java library files" in Programming  
     * with AEM Forms 
     */ 
 import java.util.Properties; 
  
 import com.adobe.idp.backup.dsc.client.BackupServiceClient; 
 import com.adobe.idp.backup.dsc.service.BackupModeEntryResult; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 public class BackupRestoreEnter 
 { 
     public static void main(String[] args)  
     { 
         try 
         { 
             // Set connection properties required to invoke AEM Forms 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,"administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
  
             // Create a ServiceClientFactory instance 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
  
             // Create a BackupService client object 
             BackupServiceClient backup = new BackupServiceClient(myFactory); 
              
             // Specify a generic label, 120 minutes to perform the backup,  
             // and not to provide continous backup mode coverage (used for snapshot backups) 
             String backUpLabel = new String("Snapshot2008July01"); 
             int minsInBackupMode = 120; 
             boolean continousCoverage = false; 
              
              
             // Enter backup mode on the forms server server 
             BackupModeEntryResult backupResult = backup.enterBackupMode(backUpLabel,minsInBackupMode, continousCoverage); 
              
             // Get information from entering backup mode on the the forms server server. 
             if (backupResult != null) 
             {     
                 System.out.println("Start time is: " + backupResult.getStartTime()); 
                 System.out.println("Backup Current ID is: " + backupResult.getId()); 
                 System.out.println("Backup Previous ID is: " + backupResult.getPreviousReservationId()); 
                 System.out.println("Backup Label is: " + backupResult.getLabel()); 
                 System.out.println("Backup Time to complete is: " + backupResult.getReservationTimeout()); 
             } 
             else 
             { 
                 System.out.println("Could not enter backup mode."); 
             } 
                              
         } 
         catch (Exception e)  
         { 
             e.printStackTrace(); 
         } 
         return; 
     }  
 } 
 
```

## Quick Start (SOAP mode): Leaving backup mode using the Java API {#quick-start-soap-mode-leaving-backup-mode-using-the-java-api}

The following Java code example explicitly causes a Forms Server to leave backup mode and return to purging files from the Global Document Storage. (See [Leaving Backup Mode on the forms server](/programming-with-aem-forms/preparing-aem-forms-backup#leaving_backup_mode_on_the_forms_server).)

```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-backup-restore-client-sdk.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
    * 4. activation.jar (required for SOAP mode) 
    * 5. axis.jar (required for SOAP mode) 
    * 6. commons-codec-1.3.jar (required for SOAP mode) 
    * 7. commons-collections-3.2.jar  (required for SOAP mode) 
    * 8. commons-discovery.jar (required for SOAP mode) 
    * 9. commons-logging.jar (required for SOAP mode) 
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
    * 12. jaxrpc.jar (required for SOAP mode) 
    * 13. log4j.jar (required for SOAP mode) 
    * 14. mail.jar (required for SOAP mode) 
    * 15. saaj.jar (required for SOAP mode) 
    * 16. wsdl4j.jar (required for SOAP mode) 
    * 17. xalan.jar (required for SOAP mode) 
    * 18. xbean.jar (required for SOAP mode) 
    * 19. xercesImpl.jar (required for SOAP mode) 
     * 
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to  
     * your local development environment and then include the 3 JBoss JAR files in your class path 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * 
     * <install directory>/jboss/bin/client 
     * 
     * If you want to invoke a remote forms server instance and there is a 
     * firewall between the client application and the server, then it is  
     * recommended that you use the SOAP mode. When using the SOAP mode,  
     * you have to include additional JAR files located in the following  
     * path 
     * <install directory>/sdk/client-libs/thirdparty 
     * 
     * For information about the SOAP  
     * mode and the additional JAR files that need to be included,  
     * see "Setting connection properties" in Programming  
     * with AEM Forms 
     * 
     * For complete details about the location of the AEM Forms JAR files,  
     * see "Including AEM Forms Java library files" in Programming  
     * with AEM Forms 
     */ 
 import java.util.Properties; 
  
 import com.adobe.idp.backup.dsc.client.BackupServiceClient; 
 import com.adobe.idp.backup.dsc.service.BackupModeResult; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 public class BackupRestoreLeave  
 { 
      
     public static void main(String[] args) 
     { 
         try 
         { 
             //Set connection properties required to invoke AEM Forms 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://[server]:[host]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,"administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
  
             // Create a ServiceClientFactory instance 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
  
             // Create a BackupService object 
             BackupServiceClient backup = new BackupServiceClient(myFactory); 
                      
             // Leave backup mode on the forms server 
             BackupModeResult leaveBackupResult = backup.leaveBackupMode(); 
              
             //Get result information from leaving backup mode 
             if (leaveBackupResult != null) 
             { 
                 System.out.println("Backup Mode ID is : " + leaveBackupResult.getId()); 
             } 
             else 
             { 
                 System.out.println("Forms server is not in backup mode."); 
             }         
      
         } 
         catch (Exception e)  
         { 
             e.printStackTrace(); 
         } 
         return; 
     } 
 } 
 
```
