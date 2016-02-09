### Remote Commands

### App Publishing Commands

### publish-app

Publishes the app to the namespace specified by the environment. This command must be run in the app folder.

Notes:

* Publish-ready app files must be located in a /www folder in the root of the app directory so that the publish-app command can zip it up and send it to the cloud.
* Need to have version, name, profile, and title specified in the package.json when publishing (use the app metadata commands and profile commands above to do this).
* LICENSE, index.html, and package.json are required and must be located in the root of the app directory.
* Only users with the admin profile are allowed to publish apps.
* Max zip file size is 20mb.
* Max number of files is 1024.
* On publish, the cloud creates the profile specified by the package.json's profile definition and then assigns the profile to the developer who published the app.

Within an application's package.json file, there is a settings object which contains valuable metadata about the application which the Global App Store and mobile container use to properly display the application.


### Informational Commands

Get data about the deployed app from the cloud.

### list-apps

This command lists all the apps that you can see in your specified environment that are currently deployed in the cloud.

##### Signature

```
> app-tools list-apps [env-options]
```

##### Arguments

None.

##### Options

See environment options above.

##### Return

A list of apps currently in the cloud. Each app entry will show its meta data.

### get-profile

This command shows the profile that is associated with your deployed app. This command must be run in the app folder.

##### Signature

```
$> app-tools get-profile [env-option]
```
##### Arguments

None.

##### Options

See environment options above.

##### Return

The profile the deployed app is currently associated with.

### Profile Commands

Remote commands dealing with the profile associated with the deployed app.

##### assign-profile-to-user

Assign the deployed app's profile to an existing user in the cloud. This command must be run in the app folder.

##### Signature

```
> app-tools assign-profile-to-user <username> [env-options]
```

##### Arguments

1. username

##### Options

See environment options above.

##### Return

The user definition.
