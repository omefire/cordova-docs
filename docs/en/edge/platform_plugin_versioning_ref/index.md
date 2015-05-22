---
license: Licensed to the Apache Software Foundation (ASF) under one
         or more contributor license agreements.  See the NOTICE file
         distributed with this work for additional information
         regarding copyright ownership.  The ASF licenses this file
         to you under the Apache License, Version 2.0 (the
         "License"); you may not use this file except in compliance
         with the License.  You may obtain a copy of the License at

           http://www.apache.org/licenses/LICENSE-2.0

         Unless required by applicable law or agreed to in writing,
         software distributed under the License is distributed on an
         "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
         KIND, either express or implied.  See the License for the
         specific language governing permissions and limitations
         under the License.
---

# Platforms and Plugins Version Management
From version 4.3.0 onwards, Cordova provides the ability to save and restore platforms and plugins. <br />
This feature allows developers to save and restore their app to a known state without having to check in all of the platform and plugin code. <br />
When a save command is issued, the config.xml file is used to reference details about platforms and plugins versions that should be used with the app. The config.xml file is later read during a 'restore' command and the appropriate versions of platforms/plugins installed.
One scenario where such capabilities come in handy is in large teams that work on an app, with each team member focusing on a platform or plugin. This feature makes it easier to share the project and reduce the amount of redundant code that is checked in the repository.


## Platform Versioning

### Saving platforms
To save a platform, you can issue the following command :

    $ cordova platform add <platform[@<version>] | directory | git_url> --save

After running the above command, the resulting config.xml might look like :

    <?xml version='1.0' encoding='utf-8'?>
        ...
        <engine name="android" spec="^4.0.0" />
        ...
    </widget>


Some examples :
  * **'cordova platform add android --save'** => retrieves the pinned version of the android platform, adds it to the project and then updates config.xml.
  * **'cordova platform add android@3.7.0 --save'** => retrieves the android platform, version 3.7.0 from npm, adds it to the project and then updates config.xml.
  * **'cordova platform add https://github.com/apache/cordova-android.git​ --save'** => clones the specified cordova-android git repository, adds the android platform to the project, then updates config.xml and point its version to the specified git-url.
  * **'cordova platform add C:/path/to/android/platform --save'** => retrieves the android platform from the specified directory, adds it to the project, then updates config.xml and point to the directory.

### Mass saving platforms on an existing project
The '--save' flag describe above is only useful when you remember to use it during the platform addition.
If you have a pre-existing project and you want to mass-save all existing platforms in it, you can use :

    $ cordova platform save


### Updating / Removing platforms
It is also possible to update/delete from config.xml during the commands 'cordova platform update' and 'cordova platform remove' :

    $ cordova platform update <platform@<version>> --save
    $ cordova platform remove <platform> --save
Some examples :
  * **'cordova platform update android --save'** => In addition to updating the android platform to the pinned version, update config.xml entry
  * **'cordova platform update android@3.8.0 --save'** => In addition to updating the android platform to version 3.8.0, update config.xml entry
  * **'cordova platform remove android --save'** => Removes the android platform from the project and deletes its entry from config.xml.


### Restoring platforms
Platforms are automatically restored from config.xml when the **'cordova prepare'** command is run.

