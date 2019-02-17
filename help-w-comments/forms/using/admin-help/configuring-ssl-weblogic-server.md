---
title: Configuring SSL for WebLogic Server
seo-title: Configuring SSL for WebLogic Server
description: Learn how to create an SSL credential for use on WebLogic server and how to configure SSL for WebLogic Server.
seo-description: Learn how to create an SSL credential for use on WebLogic server and how to configure SSL for WebLogic Server.
uuid: 6fd33722-26da-4d03-b550-67ef4ee3cf56
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 074407aa-a2f5-4d12-bf50-d30e7694a24b
index: y
internal: n
snippet: y
---

# Configuring SSL for WebLogic Server{#configuring-ssl-for-weblogic-server}

To configure SSL on WebLogic Server, you need an SSL credential for authentication. You can use Java keytool to perform the following tasks to create a credential:

* Create a public/private key pair, wrap the public key in an X.509 v1 self-signed certificate that is stored as a single-element certificate chain, and then store the certificate chain and the private key in a new keystore. This keystore is the application server’s Custom Identity keystore.
* Extract the certificate and insert it into a new keystore. This keystore is the application server’s Custom Trust keystore.

Then, configure WebLogic so that it uses the Custom Identity keystore and Custom Trust keystore that you created. Also, disable the WebLogic Hostname Verification feature because the distinguished name used to create the keystore files did not include the name of the computer that hosts WebLogic.

## Creating an SSL credential for use on WebLogic Server {#creating-an-ssl-credential-for-use-on-weblogic-server}

The keytool command is typically located in the Java jre/bin directory and must include several options and option values, which are listed in the following table.

<table cellpadding="4" cellspacing="0"> 
 <thead align="left"> 
  <tr> 
   <th class="cellrowborder" id="d19e16199" valign="top" width="NaN%"><p>Keytool option</p></th> 
   <th class="cellrowborder" id="d19e16202" valign="top" width="NaN%"><p>Description</p></th> 
   <th class="cellrowborder" id="d19e16205" valign="top" width="NaN%"><p>Option value</p></th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td class="cellrowborder" headers="d19e16199 " valign="top" width="NaN%"><p>-alias</p></td> 
   <td class="cellrowborder" headers="d19e16202 " valign="top" width="NaN%"><p>The alias of the keystore.</p></td> 
   <td class="cellrowborder" headers="d19e16205 " valign="top" width="NaN%"> 
    <ul> 
     <li><p>Custom Identity keystore: <span class="code">ads-credentials</span></p></li> 
     <li><p>Custom Trust keystore: <span class="code">bedrock</span></p></li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td class="cellrowborder" headers="d19e16199 " valign="top" width="NaN%"><p>-keyalg</p></td> 
   <td class="cellrowborder" headers="d19e16202 " valign="top" width="NaN%"><p>The algorithm to use to generate the key pair.</p></td> 
   <td class="cellrowborder" headers="d19e16205 " valign="top" width="NaN%"><p>RSA</p><p>You can use a different algorithm, depending on your company’s policy.</p></td> 
  </tr> 
  <tr> 
   <td class="cellrowborder" headers="d19e16199 " valign="top" width="NaN%"><p>-keystore</p></td> 
   <td class="cellrowborder" headers="d19e16202 " valign="top" width="NaN%"><p>The location and name of the keystore file.</p><p>The location can include the absolute path of the file. Or, it can be relative to the current directory of the command prompt where the keytool command is entered.</p></td> 
   <td class="cellrowborder" headers="d19e16205 " valign="top" width="NaN%"> 
    <ul> 
     <li><p>Custom Identity keystore: <span class="code">[</span><i>appserverdomain]</i><span class="code">/adobe/</span><i>[server name]</i><span class="code">/ads-ssl.jks</span></p></li> 
     <li><p>Custom Trust keystore: <span class="code">[</span><i>appserverdomain]</i><span class="code">/adobe/</span><i>[server name]</i><span class="code">/ads-ca.jks</span></p></li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td class="cellrowborder" headers="d19e16199 " valign="top" width="NaN%"><p>-file</p></td> 
   <td class="cellrowborder" headers="d19e16202 " valign="top" width="NaN%"><p>The location and name of the certificate file.</p></td> 
   <td class="cellrowborder" headers="d19e16205 " valign="top" width="NaN%"><span class="code"> ads-ca.cer</span></td> 
  </tr> 
  <tr> 
   <td class="cellrowborder" headers="d19e16199 " valign="top" width="NaN%"><p>-validity</p></td> 
   <td class="cellrowborder" headers="d19e16202 " valign="top" width="NaN%"><p>The number of days that the certificate is considered valid.</p></td> 
   <td class="cellrowborder" headers="d19e16205 " valign="top" width="NaN%"><p>3650</p><p>You can use a different value, depending on your company’s policy.</p></td> 
  </tr> 
  <tr> 
   <td class="cellrowborder" headers="d19e16199 " valign="top" width="NaN%"><p>-storepass</p></td> 
   <td class="cellrowborder" headers="d19e16202 " valign="top" width="NaN%"><p>The password that protects the contents of the keystore. </p></td> 
   <td class="cellrowborder" headers="d19e16205 " valign="top" width="NaN%"> 
    <ul> 
     <li><p>Custom Identity keystore: The keystore password must correspond with the SSL credential password that was specified for the Trust Store component of the Administration Console.</p></li> 
     <li><p>Custom Trust keystore: Use the same password that you used for the Custom Identity keystore.</p></li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td class="cellrowborder" headers="d19e16199 " valign="top" width="NaN%"><p>-keypass</p></td> 
   <td class="cellrowborder" headers="d19e16202 " valign="top" width="NaN%"><p>The password that protects the private key of the key pair.</p></td> 
   <td class="cellrowborder" headers="d19e16205 " valign="top" width="NaN%"><p>Use the same password that you used for the <span class="code">-storepass</span> option. The key password must be at least six characters.</p></td> 
  </tr> 
  <tr> 
   <td class="cellrowborder" headers="d19e16199 " valign="top" width="NaN%"><p>-dname</p></td> 
   <td class="cellrowborder" headers="d19e16202 " valign="top" width="NaN%"><p>The distinguished name that identifies the person who owns the keystore.</p></td> 
   <td class="cellrowborder" headers="d19e16205 " valign="top" width="NaN%"><p><span class="code">"CN=</span><span class="code">[User name]</span><span class="code">,OU=</span><span class="code">[Group Name]</span><span class="code">, O=</span><span class="code">[Company Name]</span><span class="code">, L=</span><span class="code">[City Name]</span><span class="code">, S=</span><span class="code">[State or province]</span><span class="code">, C=</span><span class="code">[Country Code]</span><span class="code">"</span></p> 
    <ul> 
     <li><p><span class="code"><i>[User name]</i></span> is the identification of the user who owns the keystore.</p></li> 
     <li><p><span class="code"><i>[Group Name]</i></span> is the identification of the corporate group that the keystore owner belongs to.</p></li> 
     <li><p><span class="code"><i>[Company Name]</i></span> is your organization’s name.</p></li> 
     <li><p><span class="code"><i>[City Name]</i></span> is the city where your organization is located.</p></li> 
     <li><p><span class="code"><i>[State or province]</i></span> is the state or province where your organization is located.</p></li> 
     <li><p><span class="code"><i>[Country Code]</i></span> is the two-letter code for the country where your organization is located.</p></li> 
    </ul></td> 
  </tr> 
 </tbody> 
</table>

For more information about using the keytool command, see the keytool.html file that is part of your JDK documentation.

## Create the Custom Identity and Trust keystores {#create-the-custom-identity-and-trust-keystores}

1. From a command prompt, navigate to *[appserverdomain]*/adobe/*[server name]*.
1. Enter the following command:

   >[!NOTE]
   >
   >Replace `*[JAVA_HOME] *`*with the directory where the JDK is installed, and replace the text in italic with values that correspond with your environment.*

   For example:

   ```as3
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   The Custom Identity keystore file named ‘‘ads-credentials.jks” is created in the [*appserverdomain*]/adobe/[*server name*] directory. 

1. Extract the certificate from the ads-credentials keystore by entering the following command:

   >[!NOTE]
   >
   >Replace `*[JAVA_HOME]*` with the directory where the JDK is installed, and replace `*store*`*_* `*password*`* with the password for the Custom Identity keystore.*

   For example:

   ```as3
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   The certificate file named “ads-ca.cer” is created in the [*appserverdomain*]/adobe/[*server name*] directory. 

1. Copy the ads-ca.cer file to any host computers that need secure communication with the application server.
1. Insert the certificate into a new keystore file (the Custom Trust keystore) by entering the following command:

   >[!NOTE]
   >
   >Replace `*[JAVA_HOME]*` with the directory where the JDK is installed, and replace `*store*`*_* `*password*` and `*key*`*_* `*password*`* with your own passwords.*

   For example:

   ```as3
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

The Custom Trust keystore file named ‘‘ads-ca.jks’’ is created in the [**appserverdomain**]/adobe/[*server*] directory.

Configure WebLogic so that it uses the Custom Identity keystore and Custom Trust keystore that you created. Also, disable the WebLogic Hostname Verification feature because the distinguished name used to create the keystore files did not include the name of the computer that hosts WebLogic Server.

## Configure WebLogic to use SSL {#configure-weblogic-to-use-ssl}

1. Start the WebLogic Server administration console by typing `http://`*[host name]* `:7001/console` in the URL line of a web browser. 
1. Under Environment, in Domain Configurations, select **Servers &gt; [*server*] &gt; Configuration &gt; General**.
1. Under General, in Configuration, ensure that **Listen Port Enabled** and **SSL Listen Port Enabled** are selected. If not enabled, do the following:

    1. Under the Change Center, click **Lock & Edit** to modify selections and values.
    1. Check the **Listen Port Enabled** and **SSL Listen Port Enabled** check boxes.

1. If this server is a Managed Server, change Listen Port to an unused port value (such as 8001) and SSL Listen Port to an unused port value (such as 8002). On a stand-alone server, the default SSL port is 7002.
1. Click **Release Configuration**.
1. Under Environment, in Domain Configurations, click **Servers &gt; [*Managed Server*] &gt; Configuration &gt; General**. 
1. Under General, in Configuration, select **Keystores**.
1. Under the Change Center, click **Lock & Edit **to modify selections and values.
1. Click **Change** to to get the keystore list as drop-down list and select **Custom Identity And Custom Trust**.
1. Under Identity, specify the following values:

   **Custom Identity Keystore**: *[appserverdomain]*/adobe/*[server name]*/ads-credentials.jks, where *[appserverdomain] *is the actual path and *[server name]* is the name of the application server.

   **Custom Identity Keystore Type**: JKS

   **Custom Identity Keystore Passphrase**: *mypassword* (custom identity keystore password)

1. Under Trust, specify the following values:

   **Custom Trust Keystore File Name**: *[appserverdomain]*/adobe/*[server]*/ads-ca.jks, where *[appserverdomain] *is the actual path

   **Custom Trust Keystore Type**: JKS

   **Custom Trust Keystore Pass Phrase**: *mypassword* (custom trust key password)

1. Under General, in Configuration, select **SSL**. 
1. By default, Keystore is selected for Identity and Trust Locations. If not, change it to keystore.
1. Under Identity, specify the following values:

   **Private Key Alias**: ads-credentials

   **Passphrase**: *mypassword*

1. Click **Release Configuration**.

## Disable the Hostname Verification feature {#disable-the-hostname-verification-feature}

1. On the Configuration tab, click SSL.
1. Under Advanced, select None from the Hostname Verification list.

   If Hostname Verification is not disabled, the Common Name (CN) must contain the server host name. 

1. Under Change Center, click Lock & Edit to modify selections and values. 
1. Restart the application server.
