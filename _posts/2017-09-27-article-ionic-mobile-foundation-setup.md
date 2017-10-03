---
layout: post
title: "Creating an Ionic 3/Mobile Foundation 8 App: Setup"
date: 2017-09-27 6:43:40
image: 'http://res.cloudinary.com/kenatibm/image/upload/bo_2px_solid_rgb:dddddd/v1506035859/Developer%20Day/blog%202017/2017-09-21.png'
description: This multi-part tutorial will demonstrate how to build a simple CRUD Ionic 3 and IBM Mobile Foundation Application.
category: 'Mobile'
tags:
- Ionic 3
- Mobile Foundation
- Bluemix
twitter_text: Setup and software requirements for Ionic 3 & IBM Mobile Foundation Crud Tutorial
introduction: Setup and software requirements for Ionic 3 & IBM Mobile Foundation Crud Tutorial.
---

# Setup: Ionic 3 & IBM Mobile Foundation Crud Tutorial

This section of the tutorial will cover the setup and installation of  necessary software required for creating a mobile application using Ionic 3 and Mobile Foundation. 

It is meant for someone who is just getting started developing Mobile Applications and wants to take a hybrid approach. That doesn't mean there are not an valuable nuggets of information, however if you are an experienced developer and the required tools installed already, you can skip this part of the tutorial - although you will want to make sure have installed the Mobile Foundation Components.

Subsequent tutorials will cover the process of creating the application, see the [introduction](http://kenatibm.com/article-ionic-mobile-foundation-intro/) for more information.

## What is needed for this Tutorial
To building a mobile application using Ionic 3 and Mobile Foundation you will need the following:

* Java Developer Kit (JDK)
* nodejs
* git
* Ionic Framework
* Cordova
* Typescript
* IBM Mobile Foundation Command Line Interface (CLI)
* json-server
* Maven
* Mobile Foundation Developer Kit
* Your favorite editor

	> For this tutorial series I will be using Visual Studio Code because it is free to use an available for Windows, Unix, and Mac.

### [Optional installations](#optional)

* [Xcode](#xcode) for Mac Developers
* [Android Studio](#androidstudio)
* [Google Chrome](#chrome)

### Software I have Installed

|  Software  |  Version  |
|  ---------  |  ----------:  |
|  macOS Sierra  |  10.12.6  |
|  Java JDK  |  1.8.0_121-b13  |
|  nodejs  |  6.11.3  |
|  npm  |  3.10.10  |
|  git  |  2.8.1  |
|  Ionic CLI  |  3.12.0  |
|  Mobile Foundation CLI  |  8.0.0-2017091111  |
|  Mobile Foundation Server  |    |
|  json-server  |  0.12.0  |
|  Maven  |  3.5.0  |

## Installing Java JDK

You will need to have either version 7 or version 8 of the Java Developer Kit (JDK) installed for the Mobile Foundation Developer Kit to run and for the ability to run Maven commands. Below are links to instructions for installing Java Developer Kit version 8.

* For Windows - [Installation Instructions](https://docs.oracle.com/javase/8/docs/technotes/guides/install/windows_jdk_install.html)
* For Mac - [Installation Instructions](https://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)
* For Linux - [installation Instructions](https://docs.oracle.com/javase/8/docs/technotes/guides/install/linux_jdk.html)

Check your installation to ensure that Java has been installed by opening a terminal or command prompt (if not already open) and type the following:

```
java -version
```

## Installing [nodejs](https://nodejs.org)

If you already have node or are unsure if you have node, open a terminal or command prompt and type `node --version`.  If [nodejs](https://nodejs.org) is installed, then you should see the version echoed back.

If you do not have [nodejs](https://nodejs.org) installed, it is a fairly simple process. Open a browser and visit [nodejs.org](https://nodejs.org/en/). On the front page is a button to download the LTS, or Long Term Support, version of nodejs.

![nodejs Download](http://res.cloudinary.com/kenatibm/image/upload/bo_2px_solid_rgb:cccccc,q_auto:eco/v1506866558/blog%202017/20170927/nodejs_home.png)

> **Note:** As of the time of writing this article LTS is for version 6.11.3.

After you have completed the installation steps for [nodejs](https://nodejs.org), you can confirm the installing by checking your [nodejs](https://nodejs.org) version as mentioned above.

Installation of [nodejs](https://nodejs.org) also includes the installation of [node package manager (npm)](https://www.npmjs.com/). [npm](https://www.npmjs.com/) is a software registery that contains millions of software products and components and is essential for installing [Ionic Framework](https://ionicframework.com/), Cordova and the Mobile Foundation Command Line Utility.

### Alternative: Node Version Manager

You may at some point in your development career require the ability to have multiple versions of nodejs installed. This can be handle by installing [Node Version Manager](https://github.com/creationix/nvm) and using it to install node for you. Installing Node Version Manager is beyond the scope of this article, however I wanted to mention it as an option.

## Installing [Git](https://git-scm.com/)

[Git](https://git-scm.com/) is one of the most widely used version control systems used today. The source that I provide throughout this tutorial will be available via Git. So if you run into trouble you can always pull from git to catch up.

Installing [Git](https://git-scm.com/) is as straightforward as installing nodejs. Visit the [Git Download Site](https://git-scm.com/downloads) and download the appropriate version for your operating system. Follow the instructions to install.

![Git Download](http://res.cloudinary.com/kenatibm/image/upload/bo_2px_solid_rgb:cccccc,q_auto:eco/v1506866557/blog%202017/20170927/git_download.png)

## Installing the [Ionic Framework Command Line Utility](https://ionicframework.com/)
The [Ionic](https://ionicframework.com/) Command Line Utility is used to create, build and test mobile applications. To install the [Ionic](https://ionicframework.com/) Command Line Utility you will use the freshly installed Node Package Manager ([npm](https://www.npmjs.com/)) that came with the nodejs installation.

Open a terminal or command prompt and type the following:

```
npm install -g ionic
```

> **Note:** You may need adminstrator permissions. Under Windows you will need to open the command prompt As Administrator. For a Mac or Unix, in the terminal session you would prefix the command with `sudo`. For example `sudo npm install -g ionic`.
> 
> The version of [Ionic](https://ionicframework.com/) CLI that will be used for this tutorial is 3.12.0. To install this particular version you can type `npm install -g ionic@3.12.0`

What the `-g` parameter does is instructs [npm](https://www.npmjs.com/) to install the [Ionic](https://ionicframework.com/) Command Line Utility such that it is accessible anywhere or **g**lobally.

For more information on installing the [Ionic](https://ionicframework.com/) Command Line Utility please visit [Ionic Installation Docs](https://ionicframework.com/docs/intro/installation/).

### Alternative: Using Ionic Creator

[Ionic Creator](http://ionic.io/products/creator) has recently been updated to support [Ionic](https://ionicframework.com/) 3, however at the time of writing this tutorial it is still in an alpha release. You can read more about it on the [Ionic](https://ionicframework.com/) Blog: [Announcing Creator Ionic 3 support! (And what’s coming next)](http://blog.ionic.io/announcing-creator-ionic-3-support-and-whats-coming-next/).

Typically I will use Creator to create my screens with it's WYSIWYG drag-drop interface. Then I create a project using the command line utility (CLI) as well use the CLI to create each of the pages. Once that is down, I download the project Ionic Creator to a temporary area, unzip it, and then copy over the HTML and CSS. 

This process is a little more complex than simply downloading the project from Creator and using that project. But the reason I do that is because I like using the [Lazy Page Loading](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&ved=0ahUKEwi75oCDssXWAhXGjFQKHQJ4AEIQFggmMAA&url=http%3A%2F%2Fblog.ionic.io%2Fionic-and-lazy-loading-pt-1%2F&usg=AFQjCNFv86rQ9mWPxzkRqqFjamwm7nca3A). Lazy Page Loading helps with performance by only loading pages when they are needed.

> There is a blog [Upgrade to Ionic 3 Lazy Loading (With Script!)](https://ionicacademy.com/ionic-3-lazy-loading/) that you could use to update a project downloaded from Creator to generate the files necessary to use Lazy Page Loading. I have added it here simply as a reference.

## Installing [Cordova](https://cordova.apache.org/)

As with the installation of [Ionic](https://ionicframework.com/) , you will use [npm](https://www.npmjs.com/) to install [Cordova](https://cordova.apache.org/). [Cordova](https://cordova.apache.org/) is the component that makes your app an app. It is a bridge between the device and the JavaScript/HTML you write your application with. Visit the Cordova site for an [Architectural Overview of Cordova](https://cordova.apache.org/docs/en/latest/guide/overview/)

Open a terminal or command prompt (if not already open) and type the following:

```
npm install -g cordova
```

To confirm that [Cordova](https://cordova.apache.org/) has been installed, go to your command prompt or terminal session and type:

```
cordova -version
```

> **Note:** You may need adminstrator permissions. Under Windows you will need to open the command prompt As Administrator. For a Mac or Unix, in the terminal session you would prefix the command with `sudo`. For example `sudo npm install -g cordova`. In addition you could have installed [Ionic](https://ionicframework.com/)  and [Cordova](https://cordova.apache.org/) at the same time by typing `sudo npm install -g ionic cordova`

## Installing [Typescript](https://www.typescriptlang.org/)

[Typescript](https://www.typescriptlang.org/) adds strong typing to Javascript. This feature and [ECMAScript 6 (or ECMA-262/ECMAScript 2015 for you purists out there)](https://www.ecma-international.org/ecma-262/6.0/), in my opinion, are what makes Javascript a viable and effective programming language. Many editors now support [Typescript](https://www.typescriptlang.org/) including the [editors](#editor) mentioned below.

As with the installation of [Ionic](https://ionicframework.com/) and [Cordova](https://cordova.apache.org/), you will use [npm](https://www.npmjs.com/) to install [Typescript](https://www.typescriptlang.org/). 

Open a terminal or command prompt (if not already open) and type the following:

```
npm install -g typescript
```
To confirm that [Typescript](https://www.typescriptlang.org/) has been installed, go to your command prompt or terminal session and type:

```
tsc --version
```

> **Note:** You may need adminstrator permissions. Under Windows you will need to open the command prompt As Administrator. For a Mac or Unix, in the terminal session you would prefix the command with `sudo`. For example `sudo npm install -g typescript`.

## Installing the [IBM Mobile Foundation Command Line Interface (CLI)](https://mobilefirstplatform.ibmcloud.com/downloads/)

As with the installation of [Ionic](https://ionicframework.com/) and [Cordova](https://cordova.apache.org/), you will use [npm](https://www.npmjs.com/) to install the [IBM Mobile Foundation Command Line Interface (CLI)](https://mobilefirstplatform.ibmcloud.com/downloads/). 

Open a terminal or command prompt (if not already open) and type the following:

```
npm install -g mfpdev-cli
```

The CLI is updated on a fairly regular basis and you can confirm the latest available release by visiting the [npm site for mfpdev-cli](https://www.npmjs.com/package/mfpdev-cli). At the time of writing this blog the current version of the CLI is 8.0.2017091111.

To confirm that the [IBM Mobile Foundation Command Line Interface (CLI)](https://mobilefirstplatform.ibmcloud.com/downloads/) has been installed, go to your command prompt or terminal session and type:

```
mfpdev --version
```

> **Note:** You may need adminstrator permissions. Under Windows you will need to open the command prompt As Administrator. For a Mac or Unix, in the terminal session you would prefix the command with `sudo`. For example `sudo npm install -g mfpdev-cli`.

## Installing [json-server](https://github.com/typicode/json-server)
json-server is a tool that allows you to quickly mock up data as JSON documents and provides full REST support. What I like about it is that I can mock up my application data structures for developing my user interface without the need for creating a full-blown database. This is great for prototyping your application. I travel a lot and the server runs locally so I can always work on my app.

Again you will use [npm](https://www.npmjs.com/) to install the [json-server](https://github.com/typicode/json-server)


Open a terminal or command prompt (if not already open) and type the following:

```
npm install -g json-server
```

> **Note:** json-server is also available via Docker Hub

## Installing your Favorite Editor

Hopefully you already have a favorite editor installed. But if you do not or would like to try something new, you can visit one or more of the following sites and follow the download/installation instructions.

* [Visual Studio Code](https://code.visualstudio.com/)
* [Sublime Text](www.sublimetext.com/2)
* [Atom](https://atom.io/)
* [Webstorm](https://www.jetbrains.com/webstorm/)
* [Brackets](http://brackets.io/)

For the remainder of this tutorial series I will use [Visual Studio Code](https://code.visualstudio.com/)

![Visual Studio Code Home Page](http://res.cloudinary.com/kenatibm/image/upload/bo_2px_solid_rgb:cccccc,q_auto:eco/v1506865990/blog%202017/20170927/visual_studio_code.png)

## Installing the Mobile Foundation Developer Kit

The Mobile Foundation Developer Kit includes a ready to run server environment based on the [IBM Websphere Liberty Profile](https://developer.ibm.com/wasdev/websphere-liberty/). The Mobile Foundation application is deployed to the Liberty Profile. Mobile Foundation is an application itself and runs on various flavors of IBM Websphere as well as Tomcat.

For development purposes the Developer Kit is great as it can be used in situations where you may not have internet access. You can download the [Mobile Foundation Developer Kit](https://mobilefirstplatform.ibmcloud.com/downloads/) from the IBM Mobile Foundation Developer site. 

> **Note:** An alternative to installing the Developer Kit would be to start an instance of Mobile Foundation on Bluemix. If you have a Bluemix Account, instructions for starting Mobile Foundation on Bluemix can be found [here](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/bluemix/using-mobile-foundation/)

Download the installation option that best supports your operating system. The installer will guide you through the installation process. Once the installation is complete you can start the server to ensure that it is installed correctly.

To start the server, open a terminal or command prompt and navigate to the directory where the Mobile Foundation Developer Kit was installed.

For Mac and linux type

```
./run.sh
```

For Windows run the batch file (run.bat) by typing

```
run
```

Once the server is started, you will know that the server is ready when you see the line **'The server mfp is ready to run a smarter planet.'**, you can open the server console by opening a second terminal or command prompt and typing

```
mfpdev server console
```

This is a Mobile Foundation CLI command that will open the server console in your default browser.  If you are shown a login page, the username and password are `admin` and `admin` respectively.

![Mobile Foundation Server Console](http://res.cloudinary.com/kenatibm/image/upload/bo_2px_solid_rgb:cccccc,q_auto:eco/v1506866556/blog%202017/20170927/mobile_foundation_server_console_welcome.png)

To verify the version of the server you are running, **Click** the Settings icon in the upper right corver of the page, then **Click** About.

![About the Mobile Foundation Server Console](http://res.cloudinary.com/kenatibm/image/upload/bo_2px_solid_rgb:cccccc,q_auto:eco/v1506866556/blog%202017/20170927/about_mobile_foundation_server.png)

> **NOTE:** More of the Mobile Foundation CLI commands will be covered in future sections of the tutorial. However if you are interested in learning more about the commands now, you can type `mfpdev help` from a terminal or command prompt.

## Installing [Maven](https://maven.apache.org/)
[Maven](https://maven.apache.org/) is a build process management open source project managed by the Apache Foundation. Mobile Foundation uses [Maven](https://maven.apache.org/) as the basis for building a deploying adapters. The [Maven](https://maven.apache.org/) respository contains a number of Mobile Foundation projects that can be found [here](https://mvnrepository.com/artifact/com.ibm.mfp). The advantage of having adapters as [Maven](https://maven.apache.org/) projects is that you can extend adapters to meet you specific needs such as creating an adapter for a third party product that is not supported.

[Maven](https://maven.apache.org/) requires Java Development Kit 1.7 or above. You can review additional requirements [here](https://maven.apache.org/download.cgi).

Installing [Maven](https://maven.apache.org/) is relatively simple. Visit the [Maven Download page](https://maven.apache.org/download.cgi) and select the appropriate archive file, Windows users will most likely download the Binary zip archive while Unix (including Mac) users will download the Binary tar.gz archive.

![Maven Install](http://res.cloudinary.com/kenatibm/image/upload/bo_2px_solid_rgb:cccccc,q_auto:eco/v1507065155/blog%202017/20170927/maven_download.png)

Once the download is complete, uncompress the archive and copy/move to an accessible location on your hard disk. Add the location of the [Maven](https://maven.apache.org/) bin directory to your path and restart as necessary.  Full instructions for installing Maven can be found [here](https://maven.apache.org/install.html).


## Optional installations

### [Xcode](https://developer.apple.com/xcode/downloads/) for Mac Developers

If you have a Mac, the easiest way to install Xcode is via tha App Store. Once you have installed Xcode you will also want to get an [Apple Developer License](https://developer.apple.com/) so you can test using a device.

![Install Xcode](http://res.cloudinary.com/kenatibm/image/upload/bo_2px_solid_rgb:cccccc,q_auto:eco/v1507067546/blog%202017/20170927/xcode.png)

### [Android Studio](https://developer.android.com/studio/index.html)

An alternative to using Xcode or as a supplement, you can install Android Studio by visiting the [Android Studio Home page](https://developer.android.com/studio/index.html). **Click** the **DOWNLOAD ANDROID STUDIO** button. Once the download is complete start the installer and follow the instructions.

![Android Studio Home Page](http://res.cloudinary.com/kenatibm/image/upload/bo_2px_solid_rgb:cccccc,q_auto:eco/v1507067875/blog%202017/20170927/android_studio.png)

After the installation you will need to install sdks and configure emulator devices.

* [Create and Manage Virutal Devices](https://developer.android.com/studio/run/managing-avds.html)
* [Update Your Tools with the SDK Manager](https://developer.android.com/studio/intro/update.html#sdk-manager)

### [Google Chrome](https://www.google.com/chrome/browser/)

I like Google Chrome's Debugging capabilities. I think the developer tools are hard to beat when building hybrid mobile and web based applications. Another very simple install as it is a download and install all in one. Visit [https://www.google.com/chrome/browser/desktop/index.html](https://www.google.com/chrome/browser/desktop/index.html) and follow the instructions.

