---
author: Alfresco Documentation
---

# Using embedded APIs

Embedded APIs are used by custom extensions executed directly against the content application server.

There are three main embedded APIs:

-   **Alfresco Java Foundation API** - provides a collection of public Java interfaces to the services provided by the server. Further details can be found in the [Alfresco Wiki](http://wiki.alfresco.com/wiki/Java_Foundation_API).
-   **JavaScript API** - provides an object-oriented view of the Java Foundation API, specifically for use in JavaScript with comprehensive access to core services.
-   **Template API** - a read-only API designed to render output such as HTML, XML, JSON, and text using the FreeMarker template engine; the Template API uses an object-oriented view of the content repository in combination with templates to generate the output.

The JavaScript and Template APIs are the key building blocks for web scripts to develop the RESTful APIs.

-   **[Using the Java API to create new content](../tasks/api-java-content-create.md)**  
 This example uses the Java API `NodeService` and `ContentService` Embedded API to create new content.
-   **[Using the JavaScript API to create new content](../tasks/api-javascript-content-create.md)**  
 This example uses the JavaScript API to create new content.
-   **[Using the Template API to display properties](../tasks/api-template-props-display.md)**  
 This example uses an Embedded API \(Template API\) to display properties for a given document.

**Parent topic:**[Overview of Alfresco APIs](../concepts/API-intro.md)

