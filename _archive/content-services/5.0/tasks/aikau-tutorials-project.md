---
author: Alfresco Documentation
---

# Creating a new Aikau project

This tutorial demonstrates how to create a new Aikau project.

You need to be set up to use the [Alfresco SDK](../concepts/alfresco-sdk-install.md).

In this tutorial you will see how to create a new Aikau project using the Alfresco SDK.

1.  Make a directory for your Aikau projects. In this series of tutorials you will use aikau-projects.

2.  Run the following command:

    ```
    
                            
    mvn archetype:generate -Dfilter=org.alfresco.maven.archetype:                        
                            
                        
    ```

3.  Select the Share AMP archetype.

4.  Press Enter to select the most recent version of the archetype.

5.  For `groupId` enter `com.alfresco.tutorials`.

6.  For `artifactId` enter `simple-aikau-project`.

7.  Press **Enter** to select the most recent community build of Alfresco.

8.  Change into the simple-aikau-project directory and enter the following command:

    ```
    
                            
    mvn install                        
                            
                        
    ```

    The project will build and report back `BUILD SUCCESS`.

9.  At this point you have created a barebones Aikau project using the Share project archetype. The next step is to explore the code that has been created for you. The most convenient way to do this is to import the project into an IDE such as Eclipse. The steps for doing this in Eclipse are given here, check the documentation for your IDE if using something other than Eclipse.
10. From the Eclipse main menu select **File** \> **Import**. In the filter box start to type "Maven" and select **Existing Maven Projects**. Click **Next**.

11. Click the **Browse** button and navigate to the root of simple-aikau-project. The pom.xml file will be detected - click **Finish** to import the project.

12. The project has now been imported. You can now explore the project more easily.
13. In the Eclipse Project Explorer, expand `src/main/amp/config/alfresco/web-extension/site-webscripts/com/example/pages` and load the file simple-page.get.js into the Eclipse editor. You will see the following code:

    ```
    
                            
    model.jsonModel = {
        widgets: [{
            id: "SET_PAGE_TITLE",
            name: "alfresco/header/SetTitle",
            config: {
                title: "This is a simple page"
            }
        }, 
        {
            id: "MY_HORIZONTAL_WIDGET_LAYOUT",
            name: "alfresco/layout/HorizontalWidgets",
            config: {
                widgetWidth: 50,
                widgets: [
                    {
                        name: "alfresco/logo/Logo",
                        config: {
                            logoClasses: "alfresco-logo-only"
                        }
                    },
                    {
                      name: "example/widgets/TemplateWidget"
                    }
                ]
            }
        }]
    };                                                
    
                        
    ```

    This is the JSON model that Aikau uses to build a web page. You will now view the output generated by this JSON code.

14. Make sure you have a repository project up and running. If you are not sure how to do this consult [this tutorial](../concepts/alfresco-sdk-getting-started.md).

15. Switch back to a terminal, make sure you are in the simple-aikau-project directory, and run your project by typing `./run.sh`. \(It is possible to run the project in Eclipse, but for now running from the command line is a bit easier.\) You may need to run the command `chmod +x run.sh` in the terminal to make the script executable.

16. Once the repo and Share are up and running, you can run the sample Aikau page by entering the following into your web browser:

    ```
    
                            
    http://localhost:8081/share/page/dp/ws/simple-page                        
                            
                        
    ```

    This displays the page without the header.

17. To display the example with the normal Share header \(and footer\) and page title, type the following into your browser:

    ```
    
                        
    http://localhost:8081/share/page/hdp/ws/simple-page                    
                        
                    
    ```

18. Now, you will make a change to the JSON code and see the effect.
19. Modify the JSON code to remove the title widget and use a vertical layout, rather than the current horizontal layout:

    ```
    
                     
    model.jsonModel = {
        widgets: [
        {
            id: "MY_VERTICAL_WIDGET_LAYOUT",
            name: "alfresco/layout/VerticalWidgets",
            config: {
                widgetWidth: 50,
                widgets: [
                    {
                        name: "alfresco/logo/Logo",
                        config: {
                            logoClasses: "alfresco-logo-only"
                        }
                    },
                    {
                      name: "example/widgets/TemplateWidget"
                    }
                ]
            }
        }]
    };                 
                     
                 
    ```

20. Restart the Share process.

    **Attention:** If you take advantage of the Alfresco SDK's hot reloading support, you will not need to restart Share after you make a change to the application code. If you would like to set up to be able to do this please see the [detailed instructions here](../concepts/alfresco-sdk-rad.md). In future tutorials it will be assumed that you are set up for hot reloading of your app. That has not been assumed in this tutorial to keep things simple.

21. Once the Share process has full restarted, point your web browser at the following address again:

    ```
    
                            
    http://localhost:8081/share/page/hdp/ws/simple-page                        
                            
                        
    ```

    You will see that the widgets are now vertically aligned rather than horizontally aligned, and the title text is no longer present.


In this tutorial you have seen how to create, modify and run an Aikau project.

**Parent topic:**[Tutorials](../concepts/aikau-tutorials.md)

