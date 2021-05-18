# Build the short video console

You can build the short video console where you can play videos, view snapshots, manually review videos, and recommend videos. The short video console allows you to view and manage videos in a visualized manner. This topic describes how to build the short video console.

-   Before you build the short video console for web, you must install Node.js and the npm package manager to compile sass dependencies such as node-sass.

    **Note:**

    -   We recommend that you use Node.js 11.15.0. If you use an earlier or a later version, you may fail to install or compile sass dependencies.
    -   We recommend that you use nvm to manage Node.js environments. nvm allows you to install different versions of Node.js environments and switch between the versions in a quick manner. You can run the `node -v` command in a command-line interface \(CLI\) to view the version of the current Node.js environment.
    -   We recommend that you install Node.js environments on a local computer. After you configure and test the console, package the source code and upload the package to your Elastic Compute Service \(ECS\) instance for publishing.
-   Before you integrate the source code of the console, you must integrate the AppServer and keep the AppServer running. For more information about how to build the AppServer, see [Build the short video AppServer](/intl.en-US/Short Video Solution/Build the short video AppServer.md).

## Overview of the short video console

The short video console has the following features:

-   Sets a request interceptor to process logon requests or request users whose logon expires to log on again.
-   Lists all videos and allows you to:
    -   Query videos based on the video ID, user ID, username, video title, review status, and creation date.
    -   View video information, including the video duration, video size, and video ID.
    -   Play videos in different resolutions and view the video description.
    -   Display snapshots.
    -   Check the review status and transcoding status.
    -   Recommend, review, transcode, and delete videos.
-   Lists recommend videos and allows you to:
    -   Query videos based on the video ID, user ID, username, video title, and creation date.
    -   View video information, including the video duration, video size, and video ID.
    -   Play videos in different resolutions and view the video description.
    -   Check the review status and transcoding status.
    -   Prefetch videos, cancel recommendation, and transcode videos by using Narrowband HD™.

## Procedure

1.  Download the source code of the short video demo.

    1.  To build the short video console, you must download the source code of the short video AppServer and console demos. For more information, see [SDK download](https://www.alibabacloud.com/help/doc-detail/51992.htm?spm=a2c63.p38356.879954.4.abd019e1rCGiIr#title-70x-3qd-cla).

    2.  Decompress the source code package. The `video-admin` directory contains the following directories and files:

        ```
        ├── node_modules                  // The directory of the dependencies in the Node.js environment. After you run the npm install command, all dependencies are installed in this directory.
        ├── dist                          // The directory of packaged project files.
        ├── public                        
        │   ├── favicon.ico               
        │   └── index.html                // The web page entry, where you can reference content from a Content Delivery Network (CDN), such as online JS and CSS files.
        ├── src                           // The directory of the business logic and Vue components.
        │   ├── assets                    // The directory of static resources, such as CSS files, images, and fonts.
        │   │   ├── images
        │   │   └── scss
        │   ├── components                // The directory of Vue components.
        │   │   ├── RecommendVideo.vue    // The dialog box component for recommend videos.
        │   │   └── VodPlayer.vue         // The player component.
        │   │   └── Tags.vue         // The video tags.
        │ │ └ ── VideoDot.vue // The video progress markers.
        │   │   └── VideoSort.vue         // The TV play settings.
        │   ├── mixin                     // The directory of Vue mixins.
        │   │   └── index.js
        │   ├── router-short        // The routing table configuration.
        │   │   └── index.js
        │   ├── views                     // The directory of the rendering component for the Vue router.
        │   │   ├── list                  // The rendering component for the video list router.
        │   │   │  └── index.vue
        │   │   ├── login                 // The rendering component for the logon router.
        │   │   │   └── index.vue
        │   │   ├── recommend             // The rendering component for the recommended video list router.
        │   │   │   └── index.vue
        │   │   └── videos                // The rendering component for the main page, side navigation pane, and top navigation bar.
        │   │       └── index.vue
        │   ├── App.vue                   // The main rendering component.
        │   ├── main.js                   // The main entry file.
        │   └── router.js                 // The profile of Vue router.
        ├── .browserslistrc               // The list of compatible browsers.
        ├── .gitignore
        ├── babel.config.js               // The profile of Babel.
        ├── package-lock.json
        ├── package.json                  // The package description file, which contains the information about dependencies, authors, and description.
        ├── postcss.config.js             // The profile of PostCSS, which is prefixed with the name of the CSS vendor.
        ├── README.md
        ├── README_zh.md
        └── vue.config.js                 // The profile of Vue. 
        ```

        **Note:** The source code of the short video console is in the `video-admin` directory. Therefore, you must run subsequent commands in the `video-admin` directory.

2.  Complete the required configuration and compilation.

    1.  Modify the configuration in the `./video-admin/vue.config.js` file. Set the `proxy` parameter to the public IP address of the ECS instance where the short video AppServer is built followed by the port number 8080, which is http://<Public IP address of the ECS instance\>:8080. The following code shows the configuration:

        ```
        module.exports = {
        // Specify the proxy for frontend development.
        devServer: {
         proxy: 'http://*.*.*.*:8080',    // Set this parameter to the endpoint of the ECS instance, without a forward slash (/) at the end.
        },
        productionSourceMap: false,
        // Specify the path of static resources for the production and development environments.
        publicPath: process.env.NODE_ENV === 'production'
         ? 'http://example.com/resource/'
         : '/',
        }
        ```

    2.  After you install the environment, open a command-line interface \(CLI\) and go to the `video-admin` directory. In the directory, run the following command to install project dependencies:

        ```
        npm install
        ```

    3.  After you install the required dependencies and modify the required configuration, run the following command:

        ```
        npm run server
        ```

        **Note:**

        -   After you run the preceding command, a service is started on your computer. Open the default URL http://localhost:8080 in a browser. Then, you can use the console on your local computer to review and recommend the uploaded videos. If you start the service on a server, you can open the following URL in a browser on your local computer: http://IP address of the server:8080.
        -   When you initialize the database that is created on the AppServer, a console administrator account is created by default. The username is admin, and the password is 123456. You can use this account to log on to the console.
3.  Package and release the source code.

    1.  Modify the configuration in the `./video-admin/vue.config.js` file.

        When you release the source code in the production environment, set the `publicPath` parameter in the `vue.config.js` file to the path of static resources. For example, the current project uses the `spring boot` framework as the backend. The static resources of the project are stored in the `webapp/resource/short-video` directory. Then, set the `publicPath` parameter in the `vue.config.js` file, as shown in the following code:

        ```
        module.exports = {
           // Specify the proxy for frontend development.
           devServer: {
            proxy: 'http://*.*.*.*:8080',    // Set this parameter to the endpoint of the ECS instance, without a forward slash (/) at the end.
           },
          productionSourceMap: false,
          // Specify the path of static resources for the production and development environments.
          publicPath: process.env.NODE_ENV === 'production'
            ? '/resource/short-video/'
            : '/',
        }
        ```

    2.  Go to the project directory `video-admin` and run the following packaging command:

        ```
        npm run build
        ```

        **Note:**

        -   This command compresses static resource files. The compressed source code can be released in the production environment.
        -   The project is packaged by `webpack` that is encapsulated by `Vue CLI`. You can customize `webpack` in the `vue.config.js` file. For more information, visit [Configuration Reference](https://cli.vuejs.org/zh/config/).
    3.  After you run the packaging command, packaged files are generated in the `video-admin/dist` directory with the following directories and files:

        ```
        ├──dist
           ├── css
           │   ├── app.[hash].css             // The CSS file of Vue components or the custom CSS file.
           │   └── chunk-vendors.[hash].css   // The CSS file that is imported by dependencies.
           ├── fonts
           ├── img
           ├── js
           │   ├── app.[hash].css             // The JS file of Vue components or the custom JS file.
           │   └── chunk-vendors.[hash].css   // The JS file that is imported by dependencies.
           ├── favicon.ico
           └── index.html
        ```

        **Note:** During packaging, `webpack` has separated the `CSS` and `JS` files that are imported by dependencies from custom `CSS` and `JS` files. The separation speeds up the web page response. In addition, the separation allows you to update only the `app.[hash].js` and `app.[hash].css` files during iteration if dependencies are not changed.

4.  Release the source code on the AppServer.

    1.  The project uses the `spring boot` framework as the backend. The `targetPath` parameter specifies the directory where the web console is deployed. In the demo, the directory is `resources`. To change the directory, you must modify the `targetPath` parameter of the `<resources>` tag in the `pom.xml` file.

    2.  Upload the `./video-admin/dist` directory that is packaged in the last step to the ECS instance. Store all the files in the dist directory in the `/src/main/webapp/resource/short-video/` path where the source code of the AppServer resides.

        ```
        # Upload the dist directory to the ECS instance by using the scp command. Copy all the files in the dist directory to the short-video directory.
        scp -rf Upload directory/dist/* Root directory of the AppServer source code/src/main/webapp/resource/short-video/
        ```

    3.  Repackage the AppServer source code where the console is integrated. Deploy the source code on the AppServer. Then, restart the AppServer. For more information, see [Build the AppServer](/intl.en-US/Short Video Solution/Build the short video AppServer.md).

        ```
        # Go to the root directory of the project in CLI and run the compilation and packaging command. If the AppServer is running, we recommend that you stop the service and then repackage the source code.
        mvn clean package -Dmaven.test.skip=true
        # After the source code is packaged, the sdk-api-0.0.1-SNAPSHOT.jar file is generated in the target directory that is in the root directory of the project.
        # Go to the directory of the JAR package in CLI, deploy the JAR package, and then start the AppServer.
        nohup java -jar sdk-api-0.0.1-SNAPSHOT.jar &
        ```

        **Note:** The ECS instance that you purchase may have limited idle memory. If you want to repackage and deploy the source code of the AppServer, run the `jps` command and the `kill` command to stop the service. Then, run the `mvn` command and the `java` command to repackage the source code in a JAR package and deploy the JAR package. Otherwise, the packaging may fail due to insufficient memory.

    4.  Enter the endpoint of the short video AppServer in a browser to access the web page of the console, for example, `http://<Public IP address of the ECS instance>:8080/resource/index.html` or `http://Domain name/resource/index.html`.


