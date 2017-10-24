####app-tools
app-tools is a command line tool, bundled with bodhi-cli, that allows app developers to quickly generate
an app and publish it to the cloud so that it can be installed by the developer into their namespace.

### Local Commands

### App Creation Commands

### new-app

Creates a new app skeleton in /apps folder based on the type of skeleton app specified. 

Notes:

* App name must be unique to the namespace.
* The app's profile name is the same as the app name.
* Once app name and profile name has been specified, it cannot be changed.

##### Signature

```
> app-tools new-app <app-name> [meta-data-options] [env-options]
```

##### Arguments

1. app name

##### Options

See environment options above (environment options are only needed for app-generator).

Meta Data Options:

long        | short     | arg                                 | meaning
----------- | --------- | ----------------------------------- | -------------
type        | t         | custom (default), app generator, angular   | specifies the type of skeleton project to create
model       | m         | resource type                       | specifies the resource type for the app generator function

##### Return

None.

##### Custom App

Creates a custom app skeleton in /apps/\<app-name\>.
The custom app skeleton just has the required files needed to publish the app.

```
> app-tools new-app <app-name> [meta-data-options]
```

##### Angular App

Creates an angular app skeleton in /apps/\<app-name\>.

```
> app-tools new-app <app-name> -t angular [meta-data-options]
```

##### App Generator

Creates a list-detail app based on the specified type (-m). The app will list the 20 most recent records fo the specified type. The user can then drill down and see the record in more detail. 

Notes:

* Environment information is used to grab the type definition remotely from the environment's namespace.
* The model with the select action (specified by the -m flag) will be added to the profile definition upon app creation.

```
> app-tools new-app <app-name> -t app-generator -m <type name> [meta-data-options] [env-options]
```

### Profile Definition Commands

The following commands allow the user to edit/view the local profile definition. When the user publishes the app, the cloud will create a unique profile (profile name will be the same as the app name) specifically for this app. Any user with this profile will then be able to use this app.

### Profile Action Options

long      | meaning
----      | -------
select    | select action allowed on type
update    | update action allowed on type
delete    | delete action allowed on type
insert    | insert action allowed on type
aggregate | aggregate action allowed on type


### view-profile-def

View the local app profile definition.

##### Signature

```
> app-tools view-profile-def
```

##### Arguments

None.

##### Options

None.

##### Return

The local app profile definition.

### add-type-to-profile

Add a type and its allowed actions to the local app profile definition. If the type already exists, it will overwrite it. Application type cannot be edited.

##### Signature

```
> app-tools add-type-to-profile <type> [profile-action-options]
```

##### Arguments

1. type

##### Options

See profile action options above.

##### Return

The local app profile definition.

### remove-type-from-profile

Remove a type from the local app profile definition. Application type cannot be removed.

##### Signature

```
> app-tools remove-type-from-profile <type>
```

###### Arguments

1. type

##### Options

None.

##### Return

The local app profile definition.

### App Metadata Commands

### edit-title

Edit the app title.

##### Signature

```
> app-tools edit-title <title>
```

##### Arguments

1. title

##### Options

None.

##### Return

Message stating the title has been changed to \<title\>.

### view-title

View the app title.

##### Signature

```
> app-tools view-title
```

##### Arguments

None.

##### Options

None.

##### Return

The app title.

### edit-description

Edit the app description.

##### Signature

```
> app-tools edit-description <description>
```

##### Arguments

1. description

##### Options

None.

##### Return

Message stating description has been changed to \<description\>.

### view-description

View the app description.

##### Signature

```
> app-tools view-description
```

##### Arguments

None.

##### Options

None.

##### Return

The app description.

### edit-version

Edit the app version.

##### Signature

```
> app-tools edit-version <version>
```

##### Arguments

1. version

##### Options

None.

##### Return

Message stating the app version has been changed to \<version\>.

### view-version

View the app version.

##### Signature

```
> app-tools view-version
```

##### Arguments

1. version

##### Options

None.

##### Return

The app version.


### Package.json

**General info::**

NOTES: Add configure field to package.json in the form below:

- Path references are all relative to the www/public folder

- Type references must avoid collisions with other apps; to accomplish this, types should be prefixed with some kind of publisher key which will be validated by the store at install time - this ensures that publishers clobber only the types published by them

- For "install" builds, install is normal

- If there is an upgrade property, the process is as follows:
  * find the currently installed version
  * for each version number between current version and newest version, apply each script in sequence pre-install, then post-install
  * if current version == most recent version, apply the pre-install, then update the dml, then install the app, then apply post-install script
  * if current version > most recent version, apply all changes in sequence, then update dml and install app

- Upgrade json and data/scripts pertaining to a version will be maintained in the public folder under version/{version}


````
Example JSON for versioning (This is the Inventory App's package.json):

{
  "configure": {
    "version": "0.09.03",
    "install": {
      "icon": "assets/Icon_BodhiInventory.png", 
      "model": {
        "custom_types": [
          "Types/{key}-InventoryCount.json", 
          "Types/{key}-InventoryCountTypeNew.json", 
          "Types/{key}-InventoryPurchaseOrder.json", 
          "Types/{key}-InventoryVendor.json"
        ], 
        "embedded_types": [
          "Types/{key}-InventoryCountTypeNode.json", 
          "Types/{key}-InventoryProduct.json", 
          "Types/{key}-InventoryProductCount.json"
        ], 
        "enumerations": [
          "Enumerations/{key}-InventoryUOMType.json", 
          "Enumerations/{key}-InventoryPurchaseOrderStatus.json"
        ]
      }, 
      "post-install": [
        {
          "action": "POST", 
          "object": "/{key}-InventoryCountTypeDaily.json", 
          "path": "/resources/{key}-InventoryCountType"
        }, 
        {
          "action": "POST", 
          "object": "/{key}-InventoryCountTypeWeekly.json", 
          "path": "/resources/{key}-InventoryCountType"
        }, 
        {
          "action": "POST", 
          "object": "/{key}-InventoryCountTypeMonthly.json", 
          "path": "/resources/{key}-InventoryCountType"
        }, 
        {
          "action": "POST", 
          "object": "/{key}-InventoryCountTypeSpot.json", 
          "path": "/resources/{key}-InventoryCountType"
        }
      ]
    }, 
    "upgrade": [
      {
        "version":"0.02",
        "description": "change count type Type, migrate data",
        "pre-install": [
          {
            "action": "POST",
            "path": "version/0.02/Types/{key}-InventoryCountTypeNew.json"
          },
        ],
        "post-install": [
          {
            "action": "PUT", 
            "path": "/some/script/path/to/migrate/from/old/to/new"
          },
          {
            "action": "DELETE", 
            "path": "/types/{key}-InventoryCountTypeOld"
          }
        ]
      },
      {
        "version":"0.03.05",
        "description": "add recipes",
        "pre-install": [
          {
            "action": "POST",
            "path": "version/0.03/Types/{key}-InventoryRecipes.json"
          }
        ]
      },
      {
        "version":"0.07",
        "description": "we don't support recipes anymore - remove them and associated data",
        "post-install": [
          {
            "action": "DELETE", 
            "path": "/types/{key}-InventoryRecipes"
          },
          {
            "action": "DELETE", 
            "path": "/resources/{key}-InventoryRecipes"
          }
        ]
      },
      {
        "version":"0.08",
        "description": "whoops - we are collecting PII -  emergency update",
        "pre-install": [
          {
            "action": "PUT", 
            "path": "/some/script/path/to/remove/bad/data"
          }
        ]
      }
    ]
  }
}

````

````
Generic package.json example:

{ offline: true,
navigationBar: 'auto',
new_type_required: false,
single_container_app: false,
hide_from_global_store: false,
troubleshooting_url: null,
categories: [Object],
public_path: 'global_store',
screenshots: [Object],
installation_urls: [Object],
global_store_icon: 'global_store/global_store_icon.png',
"agent/job_parameters": {
"data_dir":
{ "description": "", "required": true, "type": "string", "default": "" "position": }
"agent/job_parameters_hidden": {
"data_dir":
{ "description": "", "required": true, "type": "string", "default": "" }
}
````
Use the settings JSON object to communicate the meta data about an app. See definitions below:

**offline=true/false**  

Offline controls whether the container will cache application information for offline use. If offline=true and the user launches the application, any data that was previously loaded will be available when the device is offline. This will also enable queuing of data to write to the Bodhi Cloud if the app has write permissions.

**single_container_app=true/false**  

single_container_app the container know whether the app should be displayed with a menu (a collection of apps) or as a standalone single app.
Bodhi Mobile has single_container_app = false. Bodhi Reveal has single_container_app = true

**installation_urls= {http://tools.hotschedules.io/xxxx}**

For applications with single_container_app = true, developers can provide a set of installation url's to inform customers where to download their applications from the Google Play, Apple, and Windown stores. Developers can also specifiy a hockeyapp link or any other external URL.

**hide_from_global_store=true/false**  

hide_from_global_store controls whether the app is available to the general public to see in the global app store. Apps like Settings which cannot be removed should have hide_from_global_store=true

**new_type_required=true/false**  

new_type_required tells the installer of the app in the global app store if the app will run 'out of the box' or if new custom types need to be installed on the namespace.
NOTE:: if new_type_required=true, troubleshooting_url should be required

**troubleshooting_url='http://tools.hotschedules.io/xxxx'**  

The troubleshooting_url is the URL where the customer can find additional information about how to install custom types on their namespace to get an app to function correctly. This can also be used to FAQ's or any other outbound troubleshooting you would like to provide to your customers.

**categories {}**  

The categories array allows you to give the Bodhi app store taxonomical information about how your app relates to other applications. 
Examples include financial, inventory, mangagement

**public_path'/xxx/xxx'** 

The Public Path is a location off of root that allows developers to save items that should be publically visable and available. The Public Path folder should contain screenshots and Icons that the global app store can use. The global_store_icon as well as the screenshots settings objects should all be relative paths to the public path.

**global_store_icon='/xxx/xxx.png'**  

The global_store_icon is the icon that the Global App Store will use for display purposes. This file should be included in the app folder that is published via app tools and the path should be relative to the public_path.

**screenshots{}** 

The screenshots array contains relative paths to screenshots which the Global App Store will use for display purposes. This files should be included in the app folder that is published via app tools and the path should be relative to the public_path.

**agent/job_parameters:{}** and **agent/job_parameters_hidden:{}**

The agent/job_parameters contain information about any parameters that the agent or job requires to run.  They contain data_dir formatted information containing description, a required flag, type string and an optional position which is set will position the parameter in the order set 0, 1, 2, etc if not set then the parameter will be displayed in the order it's defined. Application parameters will be saved under settings so the application should use parameters from settings.

NOTE: The hidden parameter option will not be visible to the user in the installation process but will be written under the application settings.

**data_dir:{}**

The data_dir formatted information contains a description, a required flag, type string and an optional position which is set will position the parameter in the order set 0, 1, 2, etc if not set then the parameter will be displayed in the order it's defined.


----

