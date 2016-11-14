# Nativescript Web Starter
Starter to create native mobile and web apps with single shared code base using angular and nativescript.

## Prerequisites
1. Globally installed Nativecript  - `npm install -g nativescript`
2. Globally installed Angular CLI - `npm install -g angular-cli`
3. Mac OS to build iOS app.

## Installation
1. `git clone https://github.com/shripalsoni04/nativescript-web-starter --depth=1`
2. `cd nativescript-web-starter`
3. `npm run ngxp-install` 

## Run Web application
`npm start` - This will start the application at http://localhost:4200. 

## Run iOS Application
`npm run start.ios` 

## Run Android Application
`npm run start.android`
  
## Commands
You can execute any valid command of angular-cli from `web/` folder and any valid command of nativescript-cli from `nativescript/` folder.
For convenince below are the commands which you can execute from root directory.

### Common
| Command                | Description                                                                                                                          |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| npm run ngxp-install   | Installs dependencies of web and nativescript applications. Creates symlink of x-shared folder in both web and nativescript project. |

### Web Application
| Command                | Description                                                                                                                        |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| npm start              | Starts web application at http://localhost:4200                                                                                    |
| npm run start.prod     | Starts web application in production mode. Runs uglification and minification.                                                     |
| npm run start.aot      | Performs AOT for web application templates and starts web application. (Before executing this command refer Point 1 of [Known Issues](https://github.com/shripalsoni04/ngxp-quotes-app#known-issues-and-solution))                                                            |
| npm run start.aot.prod | Performs AOT, minification, uglification and starts web application. (Before executing this command refer Point 1 of [Known Issues](https://github.com/shripalsoni04/ngxp-quotes-app#known-issues-and-solution))                                                              |
| npm run build          | Builds the web application and copy the built project in web/dist folder.                                                          |
| npm run build.prod     | Builds the web application in production mode and copy the built project in web/dist folder.                                       |
| npm run build.aot      | Performs AOT, build the project and then copy the built project in web/dist folder.                                                |
| npm run build.aot.prod | Performs AOT, prepares production build and then copy the built project in web/dist folder.                                        |
| npm test               | Runs web application and x-shared unit test cases. It will not generate code coverage report.                                      |
| npm run test-cc        | Runs web application and x-shared unit test cases and generates code coverage report.                                              |
                                      

### Nativescript Application
| Command                  | Description                                                                                                                        |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| npm run start.ios        | Runs application on iOS emulator/device                                                                                            |
| npm run start.android    | Runs application on Android emulator/device                                                                                        |
| npm run livesync.ios     | Starts application in livesync mode on iOS emulator/device.                                                                        |
| npm run livesync.android | Starts application in livesync mode on Android emulator/device.       

## Known Issues and Solution
1. Regarding AOT
  - When you prepare aot build or serve project in aot mode, make sure you comment the exclude configuration in web/src/tsconfig.json file. Because currently AOT build also trying to compile test files and failing .This is know issue and can be tracked at https://github.com/angular/angular-cli/issues/2736. Once it is resolved, we can keep this uncommented for better unit testing support.
  ```
  // "exclude": [
  //   "**/*.spec.ts",
  //   "testing/**/*.ts"
  // ]
  ```

  - **Note**: When you execute `npm test` or `npm run test-cc` commands, make sure you uncomment above lines, otherwise test cases will give errors.

2. Angular dependencies at two levels for AOT support
  - Currently we have added angular dependencies in root level package.json and web/package.json. Because, AOT does not work properly when we use path mapping and this issue is reported and can be traked at https://github.com/angular/angular-cli/issues/1732 and PR:https://github.com/angular/angular-cli/pull/2470. Once this issue is resolved we can add path mapping as shown below and remove the angular dependencies from web/package.json, so in case of any version update we just need to change the version at root directory level.

    **web/src/tsconfig.json**
    ```
    "paths": {
        "@angular/*": ["../../node_modules/@angular/*"]
      }
    ```
   
## Attributes (All are npm packages)
1. nativescript-swiss-army-knife
2. Awesome framework and toolchain of Nativescript and Angular.