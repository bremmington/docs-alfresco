---
author: Alfresco Documentation
audience: 
---

# 4. Enabling Salesforce in the Alfresco Admin Console

You'll need to copy the Salesforce consumer key and consumer secret and from your connected app into the Alfresco Admin Console. These credentials prove that Alfresco has permission to be displayed in and communicate with Salesforce.

Make sure that you've applied your AMP files, downloaded the Alfresco Content Connector app, and created a connected app, as described in the previous topics. You need administrator rights to make these changes.

1.  In your Salesforce Setup menu, under Administer, click the connected app name in Manage Apps \> Connected Apps that you created in [3. Configuring your app in Salesforce](salesforce-ent-configure.md).

    In the API \(Enable OAuth Settings\) section, you'll see entries for the consumer key and consumer secret.

2.  Copy the code in the Consumer Key field.

3.  In a separate browser window, log on to the Salesforce page of the Alfresco Admin Console with your administrator credentials:

    ```
    http://localhost:8080/alfresco/service/enterprise/admin/admin-salesforce
    ```

    where localhost:8080 is your Alfresco host name and port.

4.  In the Admin Console window, paste your Salesforce consumer key into Salesforce Consumer Token.

5.  In the Salesforce window, click Click to reveal to reveal the consumer secret, and copy the code.

6.  Paste your Salesforce consumer secret into Salesforce Consumer Secret.

    You can optionally hide the password when you have pasted it into the Admin Console.

7.  Select the Salesforce Environment type that Alfresco should use. There are two options: Production \(the default value\) and Sandbox.

8.  You can optionally change the list size of records that are displayed.

    Enter a number in Recently Viewed Records List Size to specify how many recent Salesforce records are displayed when you link an Alfresco file or folder with a record. The default setting is 20 records.

    **Note:** Alternatively, you can set this in your alfresco-global.properties file using sfdc.canvas.recordMruSize. For example:

    ```
    sfdc.canvas.recordMruSize=10
    ```

9.  Save your settings.


**Parent topic:**[Installing Alfresco Content Connector for Salesforce - Classic](../concepts/salesforce-classic-ent-install-overview.md)

