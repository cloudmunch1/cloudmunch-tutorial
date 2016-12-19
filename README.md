# CloudMunch Tutorial

## Introduction
This document will help you learn how to add your own custom functionality to CloudMunch through a step-by-step process. 

## Intended audience
A developer who wants to install CloudMunch locally, try it out and extend it with his own functionality

## Pre-requisites
 - Basic working knowledge of Docker

## Table of Contents
 - [Install CloudMunch Locally](#install-cloudmunch-locally)
 - [Plugins](#plugins)
 	- [Hello World Plugin v1](#hello-world-plugin-v1)

## Install CloudMunch Locally

## Plugins
Adding a plugin to CloudMunch is easy! All you need to do is create a bunch of files and then use docker-compose to rebuild CloudMunch services

### Hello World Plugin v1
Lets start with the simplest plugin possible: one that simply logs "Hello world" into the log and exits. 

- Download the contents of the folder [hello-world-plugin-v1](examples/plugin_hello_world_v1) to the folder "plugins" inside the cloudmunch installation folder. The folder structure should now look like this:

![Folder structure](screenshots/hello-world-plugin-v1/folder_structure.png)

- Switch to the command prompt, navigate to the CloudMunch installation folder and rebuild CloudMunch services 

```bash
docker-compose down;docker-compose build;docker-compose up -d
```

![Rebulding CloudMunch](screenshots/docker-commands/rebuild-cloudmunch.gif)

- Once CloudMunch is up, create a new task and try to add this plugin to the task. 

![Add the plugin](screenshots/cm-operations/add-plugin.gif)

**Troubleshooting** If you don't see the plugin in the list, it may be because the JSON is not well formed or because of caching. Verify the JSON and clear cache http://&lt;your_host&gt;:8000/api/reset

- Edit the step, add the phrase you want to see, run the task and check the logs. You should see the phrase you entered in the logs. 

![Edit and run the task](screenshots/hello-world-plugin-v1/edit_and_run_task.gif)

*(Run the task with different inputs to verify that the phrase you enter is what is displayed in the logs)*

#### Plugin files
Lets understand the files within the [hello-world-plugin-v1](examples/plugin_hello_world_v1/hello_world) folder. Each of the files you will find in the folder are explained in detail below:

##### plugin.json:
A definition of the plugin used by the CloudMunch UI. The file should contain information and input fields which will be used to configure the plugin before execution

##### src/&lt;Name&gt;.class.php
Actual logic necessary to perform the plugin's task

##### composer.json
Composer file. Used to install the plugin and any of its dependencies

##### install.sh
Installs your plugin. You will typically never need to edit this file and can copy it from any other existing plugin


