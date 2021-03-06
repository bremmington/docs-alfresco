---
author: [Alfresco Documentation, Alfresco Documentation]
---

# LockService

A node-level locking service, used by the CheckOutCheckIn service. Does not create a working copy.

|Information|LockService|
|-----------|-----------|
|Support Status|[Full Support](http://docs.alfresco.com/support/concepts/su-product-lifecycle.html)|
|Architecture Information|[Platform Architecture](../concepts/dev-platform-arch.md)|
|Description|If you need a node-level locking system, then the LockService can provide this. Functionality provided by the service includes: -   Checking for a lock on a node
-   Obtaining lock information
-   Locking and unlocking a node
-   Suspend and enable locks

|
|Deployment - App Server|It is not likely that you will deploy Java extensions directly into a Tomcat application server as classes and Spring context files. Use an SDK build project instead.|
|[Deployment All-in-One SDK project](../concepts/sdk-getting-started.md).|-   Java source code: aio/platform-jar/src/main/java/\{domain specific package path\}
-   Spring beans: aio/platform-jar/src/main/resources/alfresco/module/platform-jar/context/service-context.xml

|
|Java API|[Java API documention](http://dev.alfresco.com/resource/AlfrescoOne/5.1/PublicAPI/org/alfresco/service/cmr/lock/LockService.html)|
|Java example|```


/** 
 * Return whether a Node is currently locked
 * @param node             The Node wrapper to test against
 * @param lockService      The LockService to use
 * @return whether a Node is currently locked
 */
public static Boolean isNodeLocked(Node node,LockService lockService){
  Boolean locked=Boolean.FALSE;
  if (node.hasAspect(ContentModel.ASPECT_LOCKABLE)) {
    LockStatus lockStatus=lockService.getLockStatus(node.getNodeRef());
    if (lockStatus == LockStatus.LOCKED || lockStatus == LockStatus.LOCK_OWNER) {
      locked=Boolean.TRUE;
    }
  }
  return locked;
}

               
```

|
|More Information|-   [Java API - Access and Transaction Management documentation](dev-extension-points-public-java-api.md).

|

**Parent topic:**[Public Java API services](../concepts/dev-services.md)

