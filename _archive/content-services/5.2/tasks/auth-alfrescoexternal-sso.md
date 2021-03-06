---
author: [Alfresco Documentation, Alfresco Documentation]
audience: 
---

# Configuring Alfresco Share to use an external SSO

Alfresco Share can be configured to accept a user name from an HTTP header provided by an external authentication system for Single Sign on \(SSO\).

This task assumes that you have already set up external authentication, as specified in [External configuration properties](../concepts/auth-external-props.md).

1.  Go to the Share <web-extension\> directory.

2.  Open the share-config-custom.xml file.

3.  Uncomment the second `<config evaluator="string-compare" condition="Remote">` section.

    **Note:** There are multiple Remote configuration sections in this file. If you have multiple sections in a configuration file, then the last section is used.

    In this uncommented Remote section:

    1.  Set the `alfrescoHeader` connector to use the same value that you defined for your external SSO property in [External configuration properties](../concepts/auth-external-props.md):

        Change the `<userHeader>` property to the same value as the `external.authentication.proxyHeader`. This sets the same HTTP header value for both Alfresco Share and the repository.

    2.  Set the `alfresco` endpoint to use the `alfrescoHeader` connector:

        1.  Change the `<connector-id>` value from `alfrescoCookie` to `alfrescoHeader`
        2.  Change the `<endpoint-url>` value to your Alfresco server URL; for example, http://localhost:8080/alfresco/s.
    **Note:** This is an example file. Review the entries for `userHeader`, `connector-id` and `endpoint-url`:

    ```
      <!-- 
            Overriding endpoints to reference an Alfresco server with external SSO
            enabled
            NOTE: If utilising a load balancer between web-tier and repository 
            cluster,the "sticky sessions" feature of your load balancer must be used.
                  
            NOTE: If alfresco server location is not localhost:8080 then also combine   
            changes from the"example port config" section below.
            *Optional* keystore contains SSL client certificate + trusted CAs.
            Used to authenticate share to an external SSO system such as CAS
            Remove the keystore section if not required i.e. for NTLM.
            
            NOTE: For Kerberos SSO rename the "KerberosDisabled" condition above to 
            "Kerberos"
            
            NOTE: For external SSO, switch the endpoint connector to "AlfrescoHeader" 
                  and set the userHeader to the name of the HTTP header 
                  that the external SSO uses to provide the authenticated user name.
       -->
       
       <config evaluator="string-compare" condition="Remote">
          <remote>
    
             <connector>
                <id>alfrescoHeader</id>
                <name>Alfresco Connector</name>
                <description>Connects to an Alfresco instance using header and cookie-based authentication</description>
                <class>org.alfresco.web.site.servlet.SlingshotAlfrescoConnector</class>
                <userHeader>X-Alfresco-Remote-User</userHeader>
             </connector>
    
             <endpoint>
                <id>alfresco</id>
                <name>Alfresco - user access</name>
                <description>Access to Alfresco Repository WebScripts that require user authentication</description>
                <connector-id>alfrescoHeader</connector-id>
                <endpoint-url>http://localhost:8080/alfresco/s</endpoint-url>
                <identity>user</identity>
                <external-auth>true</external-auth>
             </endpoint>
             
             <endpoint>
                <id>alfresco-feed</id>
                <parent-id>alfresco</parent-id>
                <name>Alfresco Feed</name>
                <description>Alfresco Feed - supports basic HTTP authentication via the EndPointProxyServlet</description> 
                <connector-id>alfrescoHeader</connector-id> 
                <endpoint-url>http://localhost:8080/alfresco/s</endpoint-url>
                <identity>user</identity>
                <external-auth>true</external-auth>
             </endpoint>
             
             <endpoint>
                <id>alfresco-api</id>
                <parent-id>alfresco</parent-id>
                <name>Alfresco Public API - user access</name>
                <description>Access to Alfresco Repository Public API that require user authentication.
                             This makes use of the authentication that is provided by parent 'alfresco' endpoint.</description>
                <connector-id>alfrescoHeader</connector-id>
                <endpoint-url>http://localhost:8080/alfresco/api</endpoint-url>
                <identity>user</identity>
                <external-auth>true</external-auth>
             </endpoint>
          </remote>
       </config>
    ```

    This is another example file, using the cookie session based endpoint:

    ```
      <!-- 
            Overriding endpoints to reference an Alfresco server with external SSO
            enabled
            NOTE: If utilising a load balancer between web-tier and repository 
            cluster,the "sticky sessions" feature of your load balancer must be used.
                  
            NOTE: If alfresco server location is not localhost:8080 then also combine   
            changes from the"example port config" section below.
            *Optional* keystore contains SSL client certificate + trusted CAs.
            Used to authenticate share to an external SSO system such as CAS
            Remove the keystore section if not required i.e. for NTLM.
            
            NOTE: For Kerberos SSO rename the "KerberosDisabled" condition above to 
            "Kerberos"
            
            NOTE: For external SSO, switch the endpoint connector to "AlfrescoHeader" 
                  and set the userHeader to the name of the HTTP header 
                  that the external SSO uses to provide the authenticated user name.
       -->
       
       <config evaluator="string-compare" condition="Remote">
          <remote>
             <ssl-config>
                 <keystore-path>alfresco/web-extension/alfresco-system.p12</keystore-path>
                 <keystore-type>pkcs12</keystore-type>
                 <keystore-password> alfresco-system</keystore-password>
    
                 <truststore-path> alfresco/web-extension/ssl-truststore</truststore-path>
                 <truststore-type>JCEKS</truststore-type>
                 <truststore-password>password</truststore-password>
    
                 <verify-hostname>true</verify-hostname>
             </ssl-config>   
          
             <connector>
                <id>alfrescoCookie</id>
                <name>Alfresco Connector</name>
                <description>Connects to an Alfresco instance using cookie-based 
                              authentication
                </description>
                <class>org.alfresco.web.site.servlet.SlingshotAlfrescoConnector</class>
             </connector>
    
             <endpoint>
                <id>alfresco</id>
                <name>Alfresco - user access</name>
                <description>Access to Alfresco Repository WebScripts that require user authentication</description>
                <connector-id>alfrescoCookie</connector-id>
                <endpoint-url>http://localhost:8080/alfresco/s</endpoint-url>
                <identity>user</identity>
                <external-auth>true</external-auth>
             </endpoint>
             
             <endpoint>
                <id>alfresco-api</id>
                <parent-id>alfresco</parent-id>
                <name>Alfresco Public API - user access</name>
                <description>Access to Alfresco Repository Public API that require user authentication.
                             This makes use of the authentication that is provided by parent 'alfresco' endpoint.</description>
                <connector-id>alfrescoCookie</connector-id>
                <endpoint-url>http://localhost:8080/alfresco/api</endpoint-url>
                <identity>user</identity>
                <external-auth>true</external-auth>
             </endpoint>
          </remote>
       </config>
    ```

4.  Save the file and then restart Share.

    Activating external authentication makes Alfresco Content Services accept external authentication tokens, make sure that no untrusted direct access to Alfresco HTTP or AJP ports is allowed.


You have configured Share to use an external SSO.

**Parent topic:**[Configuring external authentication](../concepts/auth-external-intro.md)

**Related information**  


[Configuring external authentication](../concepts/auth-external-intro.md)

