#Publishing Applications 

##Overview

To publish application for the IoT Platform, you need to follow a few simple steps to describe your application.  

##Publishing Your Application

To publish your application you must have the following directory structure for your application:

```
	/<app-name>/
	    	/public/
```
* Folder (npm app-name)
	- index.html (could be empty)
	- LICENSE (standard apache license file)
	- package.json (example provided below) 
	- public (folder) 
		- app icon.png
		- NewType1.json file (optional)
		- NewType2.json file (optional)
		- NewType3.json file (optional)


To publish an app into the IoT Platform you have to zip up the following:
{code}
		index.html (could be empty)
		LICENSE
		package.json
			
		folder=<public>
			app_icon.png
			NewType1.json file (optional)
			NewType2.json file (optional)
			NewType3.josn file (optional)
			...

###Example package.json for Mobile Applications
By Clicking on HS Template you get a package.zip file that is downloaded to your desktop that contains the following:

- **index.html**

	If you open this file it say Click Me and a Welcome will appear above Click Me

- **LICENSE**
	This is the apache2 license file that needs to be with all applications you plan to build
	
- **README.md**

	README.md are directions to get started developing your mobile application
	
- **image_home.png**
	Image_home.png is the background image for index.html



- **package.json**:

	This is the example package.json that you will cutomize based on your application needs.  To the right is a formatted version of the sample package.json that is included in HS Template's zip file.
	
```
package.json that gets includes with HS Template's zip file:

{
    "name": "HSappTemplate",
    "version": "0.0.0",
    "title": "HSappTemplate",
    "description": "New application Hello, World!",
    "profile": {
        "name": "HSappTemplate",
        "dml": {
            "BodhiApplication": {
                "select": {}
            }
        }
    },
    "settings": {
        "publisher": "",
        "categories": [""],
        "offline": false,
        "navigationBar": "auto",
        "type":"mobile"
    },
    "dependencies": {
        "bodhi-mobile":"*" 
        },
    "autoUpdateVersion": true
}

```
	
See Descriptions of package.json contents below to see what each packge.json entry is for:
   
{

    "name": "HSappTemplate",

    "version": "0.0.0",

    "title": "HSappTemplate",


    "description": "New application Hello, World!",

    "profile": {

        "name": "HSappTemplate",

        "dml": {

            "BodhiApplication": {

                "select": {}

            }

        }

    },

    "settings": {

        "publisher": "",

        "categories": [""],

        "offline": false,

        "navigationBar": "auto",

        "type":"mobile"

    },

    "dependencies": {

        "bodhi-mobile":"*" 

        },

    "autoUpdateVersion": true

}


###Example of Package.json for agent or job Applications

```
Example of package.json for agent or job applications:
#!javascript

{
  "name": "app-package-name",
  "version": "0.0.1",
  "title": "Application Title",
  "description": "Short Application Description.",
  "profile": {
    "name": "app-package-name",
    "dml": {
      “BodhiApplication": {
       "select": {},
       "update":{},
       "delete":{},
       "insert":{}
      },
      "NewType1": {
        "select": {}
      },
      "NewType2": {
        "select": {}
      }
    }
  },
  "settings": {
    "categories": [
      "Aloha",
      "POS"
    ],
    "publisher": "your company",
    "npm_package_name": "app-package-name",
    

if you have any related apps you want to install together::
"related-apps": [
      "bodhi.aloha-app-transactions",
      "bodhi.aloha-app-store"
    ],
    "public_path": "public",
    "global_store_icon": "public/icon.png",
   "type": "agent",    
(type can be “job”, “agent”, “mobile”, “web” )   
 "new_type_required": true,
  "install": {
"new": {
"model": [
{
"type": "enumeration",
"name": "TypeName",
"object": "Enumerations/TypeName.json"
},
{
"type": "embedded_type",
"name": "InventoryPurchaseOrder",
"object": "Types/InventoryPurchaseOrder.json"
},
{ "type": "custom_type",
"name": "TypeName2",
"object": "Types/TypeName2.json"
}
],
"post-type-install": [
{"action": "POST",
"object": "Data/DataFile.json",
"path": "/resources/DataFile"
}
]
if you have any parameters required to be used with the app we add this section:: 
 "agent_parameters": {
      "interval": {
        "description": "How often to execute a grind",
        "required": true,
        "type": "string",
        "default": "every 15 minutes",
        "position": 1
      }
    }
  },
  "autoUpdateVersion": false
}

```


### Description of package.json contents

**name="HSappTemplate" _required_**

The name of your application must match the name of the profile

**"version": "0.0.1" _required_**

Ideally this is the version of your application that gets posted as versions show for Agent Application in the Agent Event Logs so keeping this version the same as your Agent Application that is published is highly recommended.

**"title": "Application Title" _required_**

This is the title that will show on the HotSchedules Store once you publish your application to the HotSchedules Store.

**"description": "Short Application Description." _required_**

The description is the application description that will be displayed with the title for your application when displayed in the HotSchedules Store.  Description will be part of "Learn More" button. 

**"profile": {} _required_**

The profile section contains the following required sections:

- **"name": "HSappTemplate" _required_ and must match name above**
	
	The profile name must match the application name that is described in the main part of the package.json (see name="app-package-name" _required_ above)

- **"dml": {}**

	DML=Data Manipulation Language and this section describes what operations you plan to use on the schema or types within your application.  Usually you define the type and what operations you want to allow on the type such as select, update, delete, insert and/or aggregate. How you describe your DML section depends on what types you access and how you access/manipulate them.
	

**"settings":{} _required_**

The settings is the main section of package.json contains the following sections:

- **"categories": [] _optional_**

	A list of comma separated categories your application would fit into. The categories array allows you to give the HotSchedules Store taxonomical information about how your app relates to other applications. 
Examples include financial, inventory, management
	
- **"publisher": "your company" _required_**

	This is the name of your company or your name if you are self-represented.

- **"npm_package_name": "app-package-name" _required if building an Agent App or Job App_**
    

- **"related-apps": [] _optional_**
	Define the array of related applications as a comma separated based on the application(s)' global package name. 
	Example: 
		"related-apps": [
      		"bodhi.aloha-app-transactions",
      		"bodhi.aloha-app-store"
    		]
-  **"offline": false _Required for mobile application_** 

	Offline is for mobile applications and tells the mobile container (HotSchedules Passbook). Offline controls whether the container will cache application information for offline use. If offline=true and the user launches the application, any data that was previously loaded will be available when the device is offline. This will also enable queuing of data to write to the Bodhi Cloud if the app has write permissions.  
	
-  **"navigationBar": "auto"**

	NavigationBar is for mobile applications and tells the mobile container (HotSchedules Passbook) to automatically use the built in navigation bar.

- **"public_path": "public" _required_**

	Public path is the folder that hold any screenshots, icons, and/or type definitions.  The Public Path is a location off of root of your application that allows developers to save items that should be publicly visible and available. The Public Path folder should contain screenshots and Icons that the global app store can use. The global_store_icon as well as the screenshots settings objects should all be relative paths to the public path.	
	
- **"global_store_icon": "public/icon.png" _required_**

	In the settings section, Global Store Icon is your icon for your application.

- **"type": "mobile" _required_**

	In the settings section, you define the type of application (job, agent, mobile or web) you are publishing.  The "type"="job" define your application to run inside job engine through Job Engine Manager.  The "type"="agent" defines your application to run with the agent based on a defined role.  The "type"="mobile" defines your application to run in a mobile container usually HotSchedules Passbook.  The "type"="web" defines your application to run as a web application. 

	 
- **"new_type_required": true _optional_**

	In the settings section, if you are adding new types as described below, then this flag should be set to true. new_type_required tells the installer of the app in the global app store if the app will run 'out of the box' or if new custom types need to be installed on the namespace. _NOTE:: if new_type_required=true, troubleshooting_url should be required_

- **troubleshooting_url='http://tools.bodhi.space/xxxx' _NOTE:: if new_type_required=true, troubleshooting_url should be required_**

	The troubleshooting_url is the URL where the customer can find additional information about how to install custom types on their namespace to get an app to function correctly. This can also be used to FAQ's or any other outbound troubleshooting you would like to provide to your customers.



**agent_parameters/job_parameters**

Depending on your application needs, you may want to have parameters setup for your applications.  Both Agent and Job applications can take parameters.  The agent/job_parameters contain information about any parameters that the agent or job requires to run.  They contain data_dir formatted information containing description, a required flag, type string and an optional position which is set will position the parameter in the order set 0, 1, 2, etc if not set then the parameter will be displayed in the order it's defined. Application parameters will be saved under settings so the application should use parameters from settings.

NOTE: The hidden parameter option will not be visible to the user in the installation process but will be written under the application settings.

The following are examples of parameters that can be set for agent or the job applications respectively:

Agent Parameters example:

```
    "agent_parameters": {
      "config_file_path": {
        "description": "Config file location",
        "required": true,
        "type": "string",
        "default": "",
        "setting": "config_file_path"
      },
      "data_dir": {
        "description": "Folder location to save database files for the agent app",
        "required": true,
        "type": "string",
        "default": "C:/bodhiAgent/node_modules/merit-agent-labor/_xmloutput/",
        "setting": "data_dir"
      },
      "number_of_days_to_query": {
        "description": "Limit query to this number of days",
        "required": true,
        "type": "integer",
        "default": 60,
        "setting": "number_of_days_to_query"
      },
      "interval": {
        "description": "How often to execute a grind",
        "required": true,
        "type": "string",
        "default": "every 12 hours",
        "setting": "interval"
      },
      "local_storage_ignore_flag": {
        "description": "Ignore local storage and write all data",
        "required": true,
        "type": "boolean",
        "default": false,
        "setting": "local_storage_ignore_flag"
      }
    }
```

- All Parameters have the following 
This example sets up four parameters: timing_expression, brink_location, accessToken and uri.
Job Parameters example:

```
    "job_parameters": {
      "timing_expression": {
        "description": "How often to execute a job",
        "repeat": true,
        "type": "string",
        "default": "60 minutes"
      },
      "brink_location": {
        "description": "The alpha numeric string provided by the Brink POS API to identify the store location, e.g. tSm8y1TMSk7J4ZMyQBpeTg==",
        "type": "string",
        "required": true,
        "setting": "brink_location"
      },
      "accessToken": {
        "description": "The alpha numeric string provided by the Brink POS API to authenticate the user",
        "type": "string",
        "required": true,
        "setting": "accessToken"
      },
      "uri": {
        "description": "The url for the Brink POS API service e.g. https://api2.brinkpos.net/",
        "type": "string",
        "required": true,
        "setting": "uri"
      }
    }
```

**offline=true/false**  

Offline controls whether the container will cache application information for offline use. If offline=true and the user launches the application, any data that was previously loaded will be available when the device is offline. This will also enable queuing of data to write to the IoT Platform if the application has write permissions.

**single_container_app=true/false**  

single_container_app tells the container know whether the app should be displayed with a menu (a collection of apps) or as a standalone single app.
Bodhi Mobile has single_container_app = false. Bodhi Reveal has single_container_app = true

**hide_from_global_store=true/false**  

hide_from_global_store controls whether the app is available to the general public to see in the global app store. Apps like Settings which cannot be removed should have hide_from_global_store=true

**new_type_required=true/false**  

new_type_required tells the installer of the app in the global app store if the app will run 'out of the box' or if new custom types need to be installed on the namespace.
NOTE:: if new_type_required=true, troubleshooting_url should be required

**screenshots{}** 

The screenshots array contains relative paths to screenshots which the Global App Store will use for display purposes. These files should be included in the app folder that is published and the path should be relative to the public_path.

**data_dir:{}**

The data_dir formatted information contains a description, a required flag, type string and an optional position which is set will position the parameter in the order set 0, 1, 2, etc if not set then the parameter will be displayed in the order it's defined.

**"autoUpdateVersion": "false"**

This flag prevents autoUpdate version of the app each time you publish.  If you mark this false, you need to manually bump the version of the app each time you update it.  

**Example Type Definition**

This is an example of an enumeration, embedded_type and custom_type.  

_NOTE:_ All enumerations must be declared first, embedded_type must be after enumerations and custom_types have to be defined after enumerations and embedded_types: 

```
"install": {
"new": {
"model": [
{
"type": "enumeration",
"name": "TypeName",
"object": "Enumerations/TypeName.json"
},
{
"type": "embedded_type",
"name": "InventoryPurchaseOrder",
"object": "Types/InventoryPurchaseOrder.json"
},
{ "type": "custom_type",
"name": "TypeName2",
"object": "Types/TypeName2.json"
}
],
"post-type-install": [
{"action": "POST",
"object": "Data/DataFile.json",
"path": "/resources/DataFile"
}
]
```