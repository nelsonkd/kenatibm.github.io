---
layout: post
title: "Creating an Ionic 3/Mobile Foundation 8 App: The R in cRud"
date: 2017-10-21 11:59:40
image: 'http://res.cloudinary.com/kenatibm/image/upload/bo_2px_solid_rgb:dddddd/v1506035859/Developer%20Day/blog%202017/2017-10-21.png'
description: This multi-part tutorial will demonstrate how to build a simple CRUD Ionic 3 and IBM Mobile Foundation Application.
category: 'Mobile'
tags:
- Ionic 3
- Mobile Foundation
- Bluemix
twitter_text: Multi-part CRUD tutorial on Ionic 3 & IBM Mobile Foundation.
introduction: Multi-part CRUD tutorial on Ionic 3 & IBM Mobile Foundation.
---

* **Tutorial Overview**: [**Tutorial Home**](http://kenatibm.com/article-ionic-mobile-foundation-intro/)
* **Previous Article:** [The Article App](http://kenatibm.com/article-ionic-mobile-foundation-app/)

---

## What will you learn

In this portion of the tutorial you will learn;

1. How to create a project using Ionic
2. How to create a provider
3. How to create a list and detail page
4. How to display data on the list and detail pages
5. How to search a list of values
6. How to pull to refresh a list of values
7. How to use the InAppBrowser to display a URL

## Creating the Ionic Project

To start open a terminal or command prompt. I like to put all my projects in a working directory called projects. Create a Projects directory and then switch to that directory.

```
mkdir Projects
cd Projects
```

To create an Ionic project from your Projects directory type the following command:

```
ionic start articles blank
```

What the Ionic CLI did is create a blank project called article. Blank is one of many starter templates available with Ionic, for more information on the available starter templates visit the [Starter Templates](https://ionicframework.com/docs/cli/starters.html) documentation.

The CLI will grab the blank app template, install dependencies, and generate all the files necessary to start developing an app.

![Start Ionic App](http://res.cloudinary.com/kenatibm/image/upload/q_auto:eco/v1507391658/blog%202017/20171007/ionic_start.png)

## Review What Ionic Created

Open your favorite IDE, I will be using [Visual Studio Code](https://code.visualstudio.com/). Once your IDE is open, then open the project that was just created.

![Visual Studio Code](http://res.cloudinary.com/kenatibm/image/upload/q_auto:eco/v1507392349/blog%202017/20171007/visual_studio_code.png)

Notice that there are a number of files and directories created. 

```
.
├── README.md
├── config.xml
├── hooks
├── ionic.config.json
├── node_modules
├── package.json
├── resources
├── src
├── tsconfig.json
├── tslint.json
├── typings
└── www
```

### hooks directory

Hooks allow for pre and post process cordova commands. A discussion on hooks is beyond the scope of this tutorial, however if you are interested in learning more about hooks you can visit the [Cordova Hooks Page](https://cordova.apache.org/docs/en/latest/guide/appdev/hooks/)

### node_modules directory

This directory contains all the libraries and modules needed to support the application.  Typically this directory is not checked into source control as all the dependencies are stored in the package.json file. When a developer checks out an application from source control they will execute a `npm install` command and this will pull all the node modules for the application to run.

### resources directory

The resources directory contains the default icon and splash screens for the application. When adding a platform such as iOS or Android a directory is created for each platform and icons and splash screens are created.

Edit the icon.png and splash.png files to give the application a custom feel. Once the images have been updated, use the following command to generate the custom images for each platform.

```
ionic cordova resources
```

For more information on generating resources visit the [Ionic Cordova Resources Page](https://ionicframework.com/docs/cli/cordova/resources/)

### typings directory

Typings are used to make Typescript and Javascript play nice together. In the node_modules directory there is an `@angular` directory, in that directory expand the `common` directory, in there notice a typings file called `common.d.ts`. Common convention for naming typings files is `*.d.ts` most libraries will have one or more typings file.

More on this later in the tutorial, specifcally when the tutorial gets to the Mobile Foundation part of the tutorial.

### www directory

The `www` is the transpiled version of the application.

### README.md

This is where end user or developer notes and information about the application is placed using [Mark Down](https://en.wikipedia.org/wiki/Markdown). For a cheatsheet on markdown visit [here](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).

### config.xml

This is a global application configuration file. It contains things elements like the name of the application, the location of resources, etc.

### ionic.config.json

This file contains project configuration options for Ionic. For instance this is where one can set the default browser to use such as Google Chrome. I prefer the Google Chrome because of the developer tools.

To set the default browser, add the following to the JSON document

```
  "defaultBrowser" : "chrome"
```

When added to the `ionic.config.json` file should look similar to the following:

```
{
  "name": "articles",
  "app_id": "",
  "type": "ionic-angular",
  "integrations": {
    "cordova": {}
  },
  "defaultBrowser" : "chrome"
}
```

Alternatively use the `ionic config set` command from a terminal or command prompt. For example, to set the default browser to Chrome type:

```
ionic config set defaultBrowser "google chrome"
```

For more information on the `ionic config set` command visit [here](https://ionicframework.com/docs/cli/config/set/)

### package.json

The `package.json` file contains a list of dependencies for the application.  These dependencies are the libraries required for the application to run.

### tsconfig.json

The `tsconfig.json` file stores a list of typings.

### tslint.json

The `tslint.json` files contains the rules by which [TSLint](https://palantir.github.io/tslint/) will validate the source code.


The important directory for now is the **src** directory. This directory is where the uncompiled source lives. Under the src directory is the app, assets, pages and themes directory as well as few files important to build and run the application.

```
.
├── app
│   ├── app.component.ts
│   ├── app.html
│   ├── app.module.ts
│   ├── app.scss
│   └── main.ts
├── assets
│   └── icon
├── index.html
├── manifest.json
├── pages
│   └── home
├── service-worker.js
└── theme
    └── variables.scss
```

### src/app directory

The app directory contains the files for bootstrapping the application. This is the first component loaded when the application executes.

### src/assets directory

This directory is where assets such as images are stored for the application to use.

### src/pages directory

All pages will be created in the pages directroy. There is a default `home` page already created for the blank app.

### src/theme directory

Application themes as well as Ionic specfic variables. For more information on theming the application visit the [Ionic Theming Page](https://ionicframework.com/docs/theming/theming-your-app/)

### src/index.html

This file is the entry point for the application. Typically this file will not be edited.

### src/manifest.json

This is the manifest for a Progressive Web App. For more information read this [blog article](http://blog.ionic.io/navigating-the-world-of-progressive-web-apps-with-ionic-2/)

### src/service-worker.json

These elements will be transpiled from ECMAScript 6 to ECMAScript 5 when building the application later. Service workers are a specialize Web Worker. For more information visit the [Ionic Service Worker Page](https://ionicframework.com/docs/developer-resources/service-worker/)


## Add the iOS and Android platforms

By default the iOS platform is typically added to a project. I recommend removing and then re-adding the iOS platform to ensure that the curret version is added.  Open a terminal or command prompt and change to the `articles` directory (Projects/articles).

Then type

```
ionic cordova platform remove ios
```

to remove the iOS platform if it exists.  To add the iOS platform back to the project type the following:

```
ionic cordova platform add ios
```

Next add the Android platform by typing:

```
ionic cordova platform add android
```

To review the platforms that have been added and the platforms that can be added, type:

```
ionic cordova platform ls
```

The output should look like the following:

```
> cordova platform ls
✔ Running command - done!
Installed platforms:
  android 6.2.3
  ios 4.5.2
Available platforms: 
  blackberry10 ~3.8.0 (deprecated)
  browser ~4.1.0
  osx ~4.0.1
  webos ~3.7.0
```

Notice that the iOS and Android platforms have been added. Also notice the versions.

## Creating the Mock Data

JSON-server is a great tool for mocking up data for an application or if you need to develop without network access. This tutorial will use [json-server](https://github.com/typicode/json-server) to provide mock data for the application.

In the application directory `Projects/articles` create a directory called `data`. Change to that directory and create a file called `data.json`. Open the `data.json` file and add the following:

```
{
  "articles": [
    {
      "title": "IBM Mobile DeveloperWorks",
      "category": "Mobile, API",
      "favorite": false,
      "url": "http://mobilefirstplatform.ibmcloud.com/",
      "createdDate": "2017-09-20",
      "updateDate": "2017-10-03T23:01:19.786Z",
      "id": 2
    },
    {
      "title": "IBM API Connect DeveloperWorks",
      "category": "Mobile, API",
      "favorite": true,
      "url": "https://developer.ibm.com/apiconnect/",
      "createdDate": "2017-09-20",
      "updateDate": "2017-10-03T22:53:18.577Z",
      "id": 3
    },
    {
      "title": "IBM API Connect",
      "category": "API",
      "favorite": true,
      "url": "http://www-03.ibm.com/software/products/en/api-connect",
      "createdDate": "2017-09-20",
      "updateDate": "2017-09-20T23:50:54.128Z",
      "id": 4
    },
    {
      "title": "IBM Bluemix",
      "category": "Cloud",
      "favorite": true,
      "url": "https://www.ibm.com/cloud-computing/bluemix/",
      "createdDate": "2017-09-20",
      "updateDate": "2017-09-20T23:54:47.567Z",
      "id": 5
    },
    {
      "title": "IBM Cloud",
      "category": "Cloud",
      "favorite": true,
      "url": "https://www.ibm.com/cloud-computing/",
      "createdDate": "2017-09-20",
      "updateDate": "2017-09-21T00:56:45.498Z",
      "id": 6
    },
    {
      "createdDate": "2017-09-20T22:35:23.919Z",
      "favorite": true,
      "title": "Ken@IBM",
      "url": "http://www.kenatibm.com",
      "category": "Mobile",
      "id": 7,
      "updateDate": "2017-09-27T16:27:28.853Z"
    },
    {
      "createdDate": "2017-09-20T22:39:19.511Z",
      "favorite": true,
      "title": "Apple Website",
      "url": "http://www.apple.com",
      "category": "Software",
      "id": 8,
      "updateDate": "2017-09-21T13:38:47.195Z"
    }
  ]
}
```

What this file is doing is creating a database called `articles` and then creating records for each article.  This will create an endpoint called `articles` that will be able perform GET, POST, PUT, etc commands against.

To try it out, open a terminal or command prompt. Ensure you are in the data directory and type the following command:

```
json-server data.json
```

When the server is started you will see the following:

```
\{^_^}/ hi!

Loading data.json
Done

Resources
http://localhost:3000/articles

Home
http://localhost:3000

Type s + enter at any time to create a snapshot of the database
```

Open a browser and visit the Home page. This will show the available endpoints. Click the `/articles` link to view the list of articles.

To get a specific record simply add a slash and the id to the end of the url such as:

```
http://localhost:3000/articles/4
```

To stop the server simply issue a Ctrl+C.

## Creating Icons and Splash Screens
 
If you decide to create your own icon and splash screen for you app, you can do that now. Or you can download the icon and splash screen that I have created.  Make sure save them to the `resources` directory.

* [Splash screen (splash.png)](http://res.cloudinary.com/kenatibm/image/upload/v1507397959/blog%202017/20171007/splash.png)
* [Icon (icon.png)](http://res.cloudinary.com/kenatibm/image/upload/v1507397957/blog%202017/20171007/icon.png)

Once you have your desired Icon and Splash screen execute the following command from your article project directory (Projects/articles).

```
ionic cordova resources
```

The output should be similar to the following:

```
✔ Collecting resource configuration and source images - done!
✔ Filtering out image resources that do not need regeneration - done!
✔ Uploading source images to prepare for transformations - done!
✔ Generating platform resources: 32 / 32 complete - done!
✔ Modifying config.xml to add new image resources - done!
```

If you go to the `resources` directory then drill into the `ios/icon` and `ios/splash` directories you will see that your new icons and splash screens have been created for you.

> **Note:** If for some reason your files are not being generated, typically because the source files have not changed, then you can force the matter with the following command:
> 
> `ionic corodva resources --force`
> 
> Also when adding a platform, the resources are also automatically created for that platform.

## Modify `config.xml` File

Using your favorite editor, open the `config.xml` file. At the top of the you will notice tags for name, description, author, etc.  Change the name from `MyApp` to `MyArticles`. You can also change the description and author if you would like, but it is not necessary.

I changed the following:

```xml
<widget id="io.ionic.starter" version="0.0.1" xmlns="http://www.w3.org/ns/widgets" xmlns:cdv="http://cordova.apache.org/ns/1.0">
    <name>MyApp</name>
    <description>An awesome Ionic/Cordova app.</description>
    <author email="hi@ionicframework" href="http://ionicframework.com/">Ionic Framework Team</author>
```

to

```
<widget id="io.ionic.starter" version="0.0.1" xmlns="http://www.w3.org/ns/widgets" xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:mfp="http://www.ibm.com/mobilefirst/cordova-plugin-mfp">
    <name>MyArticles</name>
    <description>An sample Ionic/Cordova app. Based on http://www.concretepage.com/angular-2/angular-4-crud-example</description>
    <author email="[YOUR EMAIL ADDRESS]" href="[YOUR WEBSITE]">[YOUR NAME]</author>
```

The reason you change the name in the config.xml file, is that this is how the world sees your app. If you do not change the name, any app you create will be named MyApp.

## Create an Article Model

The article model defines the data structure of individual article records so that we can manipulate them. To create your model, for select the `src` directory and create a directory called `models`.

Next select the `models` directory and create a new file called `article-model.ts`.

Open the `article-model.ts` file, if not already open and add the following source.

```
export class ArticleModel {
    public id:number;
    public title: string;
    public category: string;
    public favorite: boolean;
    public url: string;
    public createdDate: Date;
    public updateDate: Date;

    constructor(){
    }
}
```

What was added are the class attributes and the `constructor` method. At a minimum every class that is create needs to have the class defined with a export and a cosntructor method. Actually, a `constructor` method is not required it is just a good practice.

You will update the constuctor in a future tutorial for now **Save** the file and go to the next step.

![Create Article Model](http://res.cloudinary.com/kenatibm/image/upload/q_auto:eco/v1508791298/blog%202017/20171007/create_article_model_file.png)


## Create the Article Provider

Ionic provides an asset [generator](https://ionicframework.com/docs/cli/generate/) as part of the  command line utility. This is a handy tool for generating pages, providers, and more.  For this tutorial you will focus on two of the most important assets - pages and providers.

Providers come as a core part of Angular, which up until recently is the primary framework used for coding the application. A provider is some configurable service that provides access to information, for instance an HTTP request or set of requests that interact with a backend system. Think of your provider as a controller of the model you created previously.

To create a provider you use the [`ionic generate`](https://ionicframework.com/docs/cli/generate/) command.

### Creating the Article Provider

Ensure that you are in your project directory `~/Projects/articles`. Then type the following:

```
ionic generate provider ArticleProvider
```

Alternatively you can use the short hand version

```
ionic g provider article
```

You should see `[OK] Generated a provider named article!` when done. However if you get a message like the following:

```
[INFO] The Ionic CLI has an update available (3.13.2 => 3.14.0)!

[WARN] No write permissions for global node_modules--automatic CLI updates are disabled.

       To fix, see https://docs.npmjs.com/getting-started/fixing-npm-permissions

       Or, install the CLI update manually:

       npm i -g ionic@latest

[OK] Generated a provider named article!
```

It simply means that you have to update your version of the Ionic Comand-Line-Interface. It is super simple to update Ionic using npm.

For Mac or Linux users you run the terminal session

```
sudo npm i -g ionic@latest
```

and for Windows users open a command prompt as Administrator and type:

```
npm i -g ionic@latest
```

Once the 

### What just happend?

At the end of running the generate commmand you will see a message that the provider has been created. So what did Ionic do for you?

First Ionic created the `providers` directory if it didn't already exist. Next it created a directory for the article provider. Then it created the article.js file.

```javascript
import { Injectable } from '@angular/core';
import { Http } from '@angular/http';
import 'rxjs/add/operator/map';

/*
  Generated class for the ArticleProvider provider.

  See https://angular.io/guide/dependency-injection for more info on providers
  and Angular DI.
*/
@Injectable()
export class ArticleProvider {

  constructor(public http: Http) {
    console.log('Hello ArticleProvider Provider');
  }

}
```

### Adding the source code to retrieve data

If you go to your `src/app` directory and open the `app.module.ts` file you will see that a couple of more things were done for you. First an import statement was added to load the `ArticleProvider`. Then the `ArticleProvider` was added to the bottom of your list of providers.

```javascript
  .
  .
  .
import { ArticleProvider } from '../providers/article/article';
  .
  .
  .
 providers: [
    StatusBar,
    SplashScreen,
    {provide: ErrorHandler, useClass: IonicErrorHandler},
    ArticleProvider
  ]
```

What Ionic will do when the app runs is instantiate the ArticleProvider for you and make it available for [dependancy injection](https://angular.io/guide/dependency-injection) throughout your app. [Dependancy injection](https://angular.io/guide/dependency-injection) is a cool trick that allows you to pass a singleton around the application for use instead of constantly having to instantiate an object.

However there will be a problem. You also need to import the HttpModule library from `@angular/http`, otherwise you will get a build error.

```javascript
  .
  .
  .
import { HttpModule } from '@angular/http';
  .
  .
  .
 imports: [
    IonicModule.forRoot(MyApp),
    HttpModule
  ],
```

And finally remove the references to the HomePage. Both the import statement and the declarations and entryComponents array.  Your `app.module.ts` should look like the following:

```javascript
import { BrowserModule } from '@angular/platform-browser';
import { ErrorHandler, NgModule } from '@angular/core';
import { IonicApp, IonicErrorHandler, IonicModule } from 'ionic-angular';
import { SplashScreen } from '@ionic-native/splash-screen';
import { StatusBar } from '@ionic-native/status-bar';

import { MyApp } from './app.component';
import { ArticleProvider } from '../providers/article/article';

import { HttpModule } from '@angular/http';

@NgModule({
  declarations: [
    MyApp
  ],
  imports: [
    BrowserModule,
    IonicModule.forRoot(MyApp),
    HttpModule
  ],
  bootstrap: [IonicApp],
  entryComponents: [
    MyApp
  ],
  providers: [
    StatusBar,
    SplashScreen,
    {provide: ErrorHandler, useClass: IonicErrorHandler},
    ArticleProvider
  ]
})
export class AppModule {}
```


You will see how to use the ArticleProvider once you get to creating the pages for the later in the tutorial.

> **Note:** one of the things I do is rename the typescript file to add the `-provider` to the file name. For instance `article.ts` becomes `article-provider.ts`. If you do make the same change, then you will need to also update the import statement in the app.module.ts file to 
> `import { ArticleProvider } from '../providers/article/article-provider';`.
> The reason I like to do this is because it makes it immediate recognizable in my editor and I know that I am editing the provider file and not the model file. But it is not a necessary modification and for this tutorial I will leave the filename the default that was generated.

Open the `src/providers/article/article.ts` file if not already open. It should look similar to the following:

```javascript
import { Injectable } from '@angular/core';
import { Http } from '@angular/http';
import 'rxjs/add/operator/map';

/*
  Generated class for the ArticleProvider provider.

  See https://angular.io/guide/dependency-injection for more info on providers
  and Angular DI.
*/
@Injectable()
export class ArticleProvider {

  constructor(public http: Http) {
    console.log('Hello ArticleProvider Provider');
  }

}
```

There are number of things that will be done. However what we want to happen at this stage is for the provider to retrieve the data and extract it or give us an exception.  We to two possibilities for how we handle this, we can handle it with a [promise](http://learnangular2.com/es6/promises) or an [observable](https://angular-2-training-book.rangle.io/handout/observables/). 

I'll leave the debate about [promises vs obserables](https://angular-2-training-book.rangle.io/handout/observables/observables_vs_promises.html) up to the web to debate, but I like observables. Observables notify my code when some piece of information has changed. This could be a refresh of a collection of data items or a user entering some data.  The point is once subscribed my components are updated automagically - well almost.

First start by adding the libraries needed to execute an HTTP request. Http is already there, but you will also need the `Response`, `Headers`, and `RequestOptions` libraries from `@angular/http`.

```javascript
import { Http, Response, Headers, RequestOptions } from '@angular/http';
```

Next add the libraries required to suport Observables:

```javascript
import { Observable } from 'rxjs';
```

Also add an import for the ArticleModel:

```javascript
import { ArticleModel } from '../../models/article-model';
```

Next add a couple of variables for the url, headers, and header options under the class export.

```javascript
  articleURL = "http://localhost:3000/articles";
  private cpHeaders = new Headers({ 'Content-Type' : 'application/json'});
  private options = new RequestOptions ({ headers : this.cpHeaders });
```

> **Note:** Rember that you will be using json-sever to handle your http traffic. If you changed the port at startup, you will need to also modify the port for the `articleURL`.

Next add three methods; one to get all of the articles, and then two helper methods.

```javascript
  getAllArticles(): Observable<Article[]> {
    return this.http.get(this.articleURL)
      .map(this.extractData)
      .catch(this.handleError);
  }

  private extractData(res:Response) {
    let body = res.json();
    return body;
  }

  private handleError(error: Response | any) {
    console.error(error.message || error);
    return Observable.throw(error.status);
  }
```
When done your code should look like the following:

```javascript
import { Injectable } from '@angular/core';
import { Http, Response, Headers, RequestOptions } from '@angular/http';
import { Observable } from 'rxjs';
import 'rxjs/add/operator/map';

import { ArticleModel } from '../../models/article-model';

@Injectable()
export class ArticleProvider {
  articleURL = "http://localhost:3000/articles";
  private cpHeaders = new Headers({ 'Content-Type' : 'application/json'});
  private options = new RequestOptions ({ headers : this.cpHeaders });

  constructor(public http: Http) {
  }

  getAllArticles(): Observable<ArticleModel[]> {
    return this.http.get(this.articleURL)
      .map(this.extractData)
      .catch(this.handleError);
  }

  private extractData(res:Response) {
    let body = res.json();
    return body;
  }

  private handleError(error: Response | any) {
    console.error(error.message || error);
    return Observable.throw(error.status);
  }
}
```

The `getAllArticles()` method will return an Observable version of an array of ArticleModel classes. It uses the `extractData` method to parse the JSON value out of the response and then map the returned values to an array of ArticleModel classes if successful. Otherwise it throws an observable error message if there is an error.

## Create a Article List Page

To create the Article List page, or the page that shows a list of the articles, you will use the Ionic generator](https://ionicframework.com/docs/cli/generate/) command again only this time you will specify a page.

Open a terminal or command prompt if not already open and type:

```
ionic generate page article-list
```

### What just happened?

Ionic created a directory and four files; the `article-list` directory which contains:

* `article-list.html` - the HTML source for the page, 
* `article-list.module.ts` - the page bootstrap information and lazy loading (more on that in a minute), 
* `article-list.scss` - the style sheet information for the page, and
* `article-list.ts` - the typescript source file.

> **Note:** [Lazy loading](http://blog.ionic.io/ionic-and-lazy-loading-pt-1/) was introduced with version 3.0 of Ionic as a beta feature. What a developer had to do prior to that is import the page and define the page as a resource similar to how a provider is defined in the `app.module.ts` file. Without lazy loading, pages were loaded at start up and could impact performance.  With [lazy loading](http://blog.ionic.io/ionic-and-lazy-loading-pt-1/) the page is only loaded if and when it is needed.



![Created Article List Page](http://res.cloudinary.com/kenatibm/image/upload/q_auto:eco/v1508798603/blog%202017/20171007/create_article_list_page.png)

Open the `article-list.html` file, it should look similar to the following:

```html
<!--
  Generated template for the ArticleListPage page.

  See http://ionicframework.com/docs/components/#navigation for more info on
  Ionic pages and navigation.
-->
<ion-header>

  <ion-navbar>
    <ion-title>article-list</ion-title>
  </ion-navbar>

</ion-header>


<ion-content padding>

</ion-content>
```

There are number of features you will add including:

* A header with a title
* A drop-down refresh
* A search control
* A list for the list of articles to be displayed

### Adding a header with a title

Open the `article-list.html` file if not already open and replace the existing code with the following:

```html
<ion-header>
  <ion-navbar color="primary">
    <ion-title>
      Articles
    </ion-title>
  </ion-navbar>
</ion-header>
```

This adds a Navigation Bar and sets the backgound color to "primary". 

> **Note:** The "primary" color is defined `theme/variables.scss` file along with sceondary, danger, light, and dark values.
> 
> ```css
> // Named Color Variables
> // --------------------------------------------------
> // Named colors makes it easy to reuse colors on various components.
> // It's highly recommended to change the default colors
> // to match your app's branding. Ionic uses a Sass map of
> // colors so you can add, rename and remove colors as needed.
> // The "primary" color is the only required color in the map.
> 
> $colors: (
>   primary:    #488aff,
>   secondary:  #32db64,
>   danger:     #f53d3d,
>   light:      #f4f4f4,
>   dark:       #222
> );
> ```

### Adding the Content

Under the ending header tag, `</ion-header>` add a content tag like so:

```html
<ion-content>
	<!-- ADD REFRESHER CODE HERE -->
	
	<!-- ADD SEARCH BAR CODE HERE -->
	
	<!-- ADD LISTVIEW CODE HERE -->
</ion-content>
```

This area will be used to contain the remainder of the HTML code for this tutorial.

### Adding a Listview HTML

The first component to add to the Articles List Page is the actual [list control](https://ionicframework.com/docs/api/components/list/List/). With the `articl-list.html` file still open, add the following code between the content tags,

by replacing the `<!-- ADD LISTVIEW CODE HERE -->` with the following:

```html
  <ion-list id="articleList">
    <ion-item-sliding *ngFor="let article of allArticles" >
      <button ion-item (click)="editArticle(article)" >
        <ion-icon [name]="article.favorite ? 'star' : 'star-outline'" item-left></ion-icon>
        <h2>{{article.title}}</h2>
        <p>{{article.url}}</p>
      </button>
    </ion-item-sliding>
  </ion-list>
```

There are a number of things going on here.

1. First the `<ion-list>` tag establishes the [list control](https://ionicframework.com/docs/api/components/list/List/)
3. A button ion-item. Note the iteration through a list of articles and for each article you create the following,
4. And a favorite icon component to show that an article is a favorite or not as well as the title and url of the article.

Your HTML for `article-list.html` should now look like the following:

```html
<ion-header>
  <ion-navbar color="primary">
    <ion-title>
      Articles
    </ion-title>
  </ion-navbar>
</ion-header>
<ion-content>
  <ion-list id="articleList">
      <button ion-item *ngFor="let article of allArticles" >
        <ion-icon [name]="article.favorite ? 'star' : 'star-outline'" item-left></ion-icon>
        <h2>{{article.title}}</h2>
        <p>{{article.url}}</p>
      </button>
  </ion-list>
</ion-content>
```

> **Note:** the button element will not do anything as you have not assigned a method to it yet so it has nowhere to go. But you will use it later.

### Adding the Listview Typescript

Next you need to create the `allArticles` variable and retrieve the data using the provider created earlier so that the list of articles is displayed. Open the `src/pages/article-list/article-list.ts` file.

There are a few things that need to be added to get data to show on the listview.

1. Add import statements for `ArticleProvider`, and `Article`
1. Add an `allArticles` variable
1. Inject the imported `ArticleProvider` via the constructor
1. Create the `getAllArticles()` method
1. Call the `getAllArticles()` method when the page loads

#### Add imports

With the `article-list.ts` file open add the following import statements:

```javascript
import { ArticleProvider } from '../../providers/article/article';
import { ArticleModel } from '../../models/article-model';
```

#### Add the `allArticles` variable

You will need a variable that stores the result of retrieving data from the provider as well as a variable to hold the status code in the event of an error. Under the class export add the following:

```javapscript
  allArticles: ArticleModel[];
  statusCode: number;
```

#### Inject the provider

As mentioned earlier, when the application starts it automatically instantiates the `ArticleProvider` for you. Using dependancy injection, or DI, you can push that object into your article-list component via the constructor. Add the following to the list of constructor parameters:

```javascript
, private articleProvider: ArticleProvider
```

Don't forget the preceeding comma, the constructor should look like the following:

```javascript
  constructor(
  		public navCtrl: NavController, 
  		public navParams: NavParams, 
    	private articleProvider: ArticleProvider) {
  }
```

#### Create `getAllArticles()` method 

```javascript
  getAllArticles() {
    this.articleProvider.getAllArticles()
      .subscribe(
        data => {
          this.allArticles = data;
        },
        errorCode => this.statusCode = errorCode
      );
  }  
```

![Save](http://res.cloudinary.com/kenatibm/image/upload/b_rgb:ffff00,c_scale,co_rgb:ff0000,e_green:0,h_16,w_16/v1508963561/blog%202017/20171007/save.png) **Save** the file.

The code is pretty simple really. First the method calls the `getAllArticles()` and then it subscibes to it. The subscription is notified any time there is a change to the observable. There are two variables passed in as part of the subscription; `data` and `errorCode`. If the call was successful then the `allArticles` variable is set to the `data` value. Otherwise the `statusCode` variable is set to the `errorCode` value.

#### Call the `getAllArticles()` method

Having the method is one thing, now you need to call it.  You should have an `ionViewDidLoad()` method. You can find more on Ionic Lifecycle Events [here](http://blog.ionic.io/navigating-lifecycle-events/).

```javascript
  ionViewDidLoad() {
    console.log('ionViewDidLoad ArticleListPage');
  }
```

In the `ionViewDidLoad()` add a call to the `getAllArticles()` method you created earlier.

```javascript
    this.getAllArticles();
```

The full code for `article-list.ts` should look like the following:

```javascript
import { Component } from '@angular/core';
import { IonicPage, NavController, NavParams } from 'ionic-angular';

import { ArticleProvider } from '../../providers/article/article';
import { ArticleModel } from '../../models/article-model';

@IonicPage()
@Component({
  selector: 'page-article-list',
  templateUrl: 'article-list.html',
})
export class ArticleListPage {

  allArticles: ArticleModel[];
  statusCode: number;
  
  constructor(public navCtrl: NavController, public navParams: NavParams, 
    private articleProvider: ArticleProvider) {
  }

  ionViewDidLoad() {
    console.log('ionViewDidLoad ArticleListPage');
    this.getAllArticles();
  }

  getAllArticles() {
    this.articleProvider.getAllArticles()
      .subscribe(
        data => {
          this.allArticles = data;
        },
        errorCode => this.statusCode = errorCode
      );
  }  
}
```

![Save](http://res.cloudinary.com/kenatibm/image/upload/b_rgb:ffff00,c_scale,co_rgb:ff0000,e_green:0,h_16,w_16/v1508963561/blog%202017/20171007/save.png) **Save** the file.

#### Instantiate the page

The last thing that needs to occur before testing is to instantiate the page. Open the `src/app/app.component.ts` file. Change the line that reads:

```
  rootPage:any = HomePage;
```

to

```
  rootPage:any = 'ArticleListPage';
```

Also remove the following line:

```
import { HomePage } from '../pages/home/home';
```

Your completed app.component.ts file should look like the following:

```
import { Component } from '@angular/core';
import { Platform } from 'ionic-angular';
import { StatusBar } from '@ionic-native/status-bar';
import { SplashScreen } from '@ionic-native/splash-screen';

@Component({
  templateUrl: 'app.html'
})
export class MyApp {
  rootPage:any = 'ArticleListPage';

  constructor(platform: Platform, statusBar: StatusBar, splashScreen: SplashScreen) {
    platform.ready().then(() => {
      // Okay, so the platform is ready and our plugins are available.
      // Here you can do any higher level native things you might need.
      statusBar.styleDefault();
      splashScreen.hide();
    });
  }
}
```

![Save](http://res.cloudinary.com/kenatibm/image/upload/b_rgb:ffff00,c_scale,co_rgb:ff0000,e_green:0,h_16,w_16/v1508963561/blog%202017/20171007/save.png) **Save** the file.

### Testing

Guess what? You are ready to start testing.  First thing you need to do is start the json-server, if you have not already done so.  To start the json-server, open a terminal or command prompt and navigate to the directory where you created the `data.json` file.  Then type `json-server data.json`

You should see something like the following:

```
  \{^_^}/ hi!

  Loading data.json
  Done

  Resources
  http://localhost:3000/articles

  Home
  http://localhost:3000

  Type s + enter at any time to create a snapshot of the database
```

If, however you get the following error, that means your server is already running.

```
  \{^_^}/ hi!

  Loading data.json
  Done

  Resources
  http://localhost:3000/articles

  Home
  http://localhost:3000

  Type s + enter at any time to create a snapshot of the database
events.js:160
      throw er; // Unhandled 'error' event
      ^

Error: listen EADDRINUSE 0.0.0.0:3000
    at Object.exports._errnoException (util.js:1020:11)
    at exports._exceptionWithHostPort (util.js:1043:20)
    at Server._listen2 (net.js:1258:14)
    at listen (net.js:1294:10)
    at net.js:1404:9
    at _combinedTickCallback (internal/process/next_tick.js:83:11)
    at process._tickCallback (internal/process/next_tick.js:104:9)
    at Module.runMain (module.js:606:11)
    at run (bootstrap_node.js:389:7)
    at startup (bootstrap_node.js:149:9)
```

With the json-server running, open another terminal or command prompt and type:

```
ionic serve
```

This will start the Ionic server and launch your default browser.  The output in the terminal should look similar to the following:

```
Starting app-scripts server: --address 0.0.0.0 --port 8100 --livereload-port 35729 --dev-logger-port 53703 - Ctrl+C

to cancel
[16:37:49]  watch started ...
[16:37:49]  build dev started ...
[16:37:49]  clean started ...
[16:37:49]  clean finished in 9 ms
[16:37:49]  copy started ...
[16:37:49]  deeplinks started ...
[16:37:49]  deeplinks finished in 38 ms
[16:37:49]  transpile started ...
[16:37:52]  transpile finished in 2.95 s
[16:37:52]  preprocess started ...
[16:37:53]  copy finished in 3.13 s
[16:37:53]  preprocess finished in 96 ms
[16:37:53]  webpack started ...
[16:38:02]  webpack finished in 9.11 s
[16:38:02]  sass started ...
[16:38:03]  sass finished in 1.12 s
[16:38:03]  postprocess started ...
[16:38:03]  postprocess finished in 7 ms
[16:38:03]  lint started ...
[16:38:03]  build dev finished in 13.42 s
[16:38:03]  watch ready in 13.49 s
[16:38:03]  dev server running: http://localhost:8100/

Development server running!
Local: http://localhost:8100
External: http://10.0.1.72:8100, http://9.85.164.229:8100
```

If you get some error messages say that there are unused items, you can ignore them.

In your browser you should see a list of articles similar to the following:

![List of Articles](http://res.cloudinary.com/kenatibm/image/upload/bo_1px_solid_rgb:cccccc,q_auto:eco/v1508888452/blog%202017/20171007/browser_test.png)

> **Note:** If you are using Google Chrome you can turn on the Developer Tools and see the console log. There you will see that the `ionViewDidLoad ArticleListPage` message is displayed.
> 
> ![Console Log](http://res.cloudinary.com/kenatibm/image/upload/bo_1px_solid_rgb:cccccc,q_auto:eco/v1508949501/blog%202017/20171007/console_log.png)

### Adding a refresher

The pull to refresh, or [ion-refresher control](https://ionicframework.com/docs/api/components/refresher/Refresher/), adds the ability for the user to pull down on a content area to refresh the data. This might be useful in a situation where some other process may update information.

![Pull to refresh](http://res.cloudinary.com/kenatibm/image/upload/q_auto:eco/v1508864293/blog%202017/20171007/pull_2_refresh.png)

To add a [refresher](https://ionicframework.com/docs/api/components/refresher/Refresher/) you will need to update both the `article-list.html` and `article-list.ts` files.  Open the `article-list.html` file and place the following code right below the `<ion-content>`  and right above the `<ion-list id="articleList">` tags:

To add this feature, add the following code below the the opening `<ion-content>` tag:

```html
  <ion-refresher (ionRefresh)="getAllArticles($event)">
    <ion-refresher-content 
      pullingIcon="arrow-dropdown"
      pullingText="Pull to refresh"
      refreshingSpinner="circles"
      refreshingText="Refreshing...">
    </ion-refresher-content>
  </ion-refresher>
```

Notice that we are now passing a variable to the `getAllArticles()` method. This will require making a couple of modifications to the `article-list.ts` file. Open the `article-list.ts` file.

Update the `getAllArticles()` method to accept a parameter and process search criteria. Replace the existing `getAllArticles()` method with the following:

```javascript
  getAllArticles(refresher) {
    this.searchTerm = "";
    this.articleProvider.getAllArticles()
      .subscribe(
        data => {
          this.allArticles = data;
          if(refresher != 0) {
            refresher.complete();
          }
        },
        errorCode => this.statusCode = errorCode
      );
  }
```

Notice that there is now a refresher variable passed to the `getAllArticles()` method. What is happening is that when the method is called, the data is pulled from the database and then if the variable is not equal to 0 (zero) then the "refreshing" notice is closed once the refresh is complete. A value of 0 (zero) means that the `getAllArticles()` method was called by something other then the refresh control. Which means that you will need to update the `getAllArticles()` method call in the `ionViewDidLoad()` method like so:

```
    this.getAllArticles(0);
```

At the end of all these updates your `article-list.ts` file should look like the following:

```
import { Component } from '@angular/core';
import { IonicPage, NavController, NavParams } from 'ionic-angular';

import { ArticleProvider } from '../../providers/article/article';
import { ArticleModel } from '../../models/article-model';

@IonicPage()
@Component({
  selector: 'page-article-list',
  templateUrl: 'article-list.html',
})
export class ArticleListPage {

  allArticles: ArticleModel[];
  statusCode: number;
  
  constructor(
    public navCtrl: NavController, 
    public navParams: NavParams, 
    private articleProvider: ArticleProvider) {
      this.searchControl = new FormControl();
    }

  ionViewDidLoad() {
    console.log('ionViewDidLoad ArticleListPage');
    this.getAllArticles(0);
  }

  getAllArticles(refresher) {
    this.searchTerm = "";
    this.articleProvider.getAllArticles()
      .subscribe(
        data => {
          this.allArticles = data;
          if(refresher != 0) {
            refresher.complete();
          }
        },
        errorCode => this.statusCode = errorCode
      );
  }
}
```

![Save](http://res.cloudinary.com/kenatibm/image/upload/b_rgb:ffff00,c_scale,co_rgb:ff0000,e_green:0,h_16,w_16/v1508963561/blog%202017/20171007/save.png) **Save** the file.

#### Testing your changes

To test your changes to see that the refresh does indeed work is pretty simple. With your changes saved, edit the data/data.json file and add an additional record to the end of the array like:

```
,
      {
        "createdDate": "2017-09-20T22:39:19.511Z",
        "favorite": false,
        "title": "Google News",
        "url": "http://news.google.com",
        "category": "News",
        "id": 9,
        "updateDate": "2017-09-21T13:38:47.195Z"
      }
```

![Save](http://res.cloudinary.com/kenatibm/image/upload/b_rgb:ffff00,c_scale,co_rgb:ff0000,e_green:0,h_16,w_16/v1508963561/blog%202017/20171007/save.png) **Save** the file.

To test the app, if your Ionic server is still runing then the app should have been built and the page refreshed.  If not open a terminal or command prompt and start Ionic:

```
ionic serve
```

Go to your app in the browser and pull to refresh. You should see the newly created record. If not, you probably did not save your work, or there was an error during the compile.

![Article List Refresh](http://res.cloudinary.com/kenatibm/image/upload/bo_1px_solid_rgb:cccccc,q_auto:eco/v1508954538/blog%202017/20171007/new_article_refresher.png)


### Adding a Search Bar

To add a [search bar](https://ionicframework.com/docs/api/components/searchbar/Searchbar/) you will need to update both the `article-list.html` and `article-list.ts` files.  Open the `article-list.html` file and place the following code right below the `</ion-refresher>` and right above the `<ion-list id="articleList">` tags:

```
  <ion-searchbar 
    [formControl]="searchControl" 
    [(ngModel)]="searchTerm" 
    (ionInput)="setFilteredItems()" 
    (ionCancel)="getAllArticles(0)" 
    [showCancelButton]="shouldShowCancel">
  </ion-searchbar>
```

![Save](http://res.cloudinary.com/kenatibm/image/upload/b_rgb:ffff00,c_scale,co_rgb:ff0000,e_green:0,h_16,w_16/v1508963561/blog%202017/20171007/save.png) **Save** the file.

What is happening here is first you are defining the formControl and setting the typed value to the `searchTerm` variable. Then as a user enters information you are calling the `setFilteredItems()` method, which you still need to create. If the users presses the Cancel button, then the control calls the `getAllArticles(0)` method to retrieve the list again.

#### Updating the `article-list.ts` file

Open the `article-list.ts` file.


Add an import for the `FormControl` library, place it with the other import statements. Place these variables under the `statusCode` variable.

```javascript
import { FormControl } from '@angular/forms';
```

Next add a couple of instance variables, one for the `searchTerm` and one for the `searchControl`.

```javascript
  searchTerm: string;
  searchControl: FormControl;
```

Next, instantiate the newly defined `searchControl` in the `constructor()` method like so:

```javascript
      this.searchControl = new FormControl();
```

Next, create the `setFilteredItems()` method. Below the `getAllArticles()` method ad the following:

```javascript
  setFilteredItems() {    
    if(this.searchTerm && this.searchTerm.trim() != '') {
      this.allArticles = this.allArticles.filter(( item ) => {
        console.log(`==> SEARCH: ${item.title} ${this.searchTerm}`);
        return (item.title.toLowerCase().indexOf(this.searchTerm.toLowerCase()) > -1);
      });
    } else {
      this.getAllArticles(0);
    }
  }
```

![Save](http://res.cloudinary.com/kenatibm/image/upload/b_rgb:ffff00,c_scale,co_rgb:ff0000,e_green:0,h_16,w_16/v1508963561/blog%202017/20171007/save.png) **Save** the file.

What is happening here is first there is a check to see if there is a value to search on by trimming the `searchTerm` that the user entered. Then a filter command on the `allArticles` array by the `searchTerm` reduces the result to only items including values that meet the search criteria. If there is no `searchTerm` then a reload of the `allArticles` array is performed by calling the `getAllArticles()` method.

To test, if the Ionic server is still runing then the app should have been built and the page refreshed.  If not open a terminal or command prompt and start Ionic:

```
ionic serve
```

Test the app by typing something in the search like 'Appl'. Notice that the result has been reduced to show only one record.

![Search](http://res.cloudinary.com/kenatibm/image/upload/bo_1px_solid_rgb:cccccc,q_auto:eco/v1508960608/blog%202017/20171007/search_appl.png)

## Create the Article Detail Page

Time create a detail page and connect the list page to the detail page. As with the article-list page use the Ionic generate page command to create the article-detail page. Open a terminal or command prompt and type:

```
ionic generate page article-detail
```

or

```
ionic g page article-detail
```

There should now be a new directory under `src/pages` that is called `article-detail`. That directory should also contain 4 files similar to the ones created during the generation of the `article-list` page.

Open the article-detail.html page and replace the existing source with the following:

```html
<ion-header>
  <ion-navbar color="primary">
    <ion-title>
      Article Details
    </ion-title>
  </ion-navbar>
</ion-header>

<ion-content>
  <form [formGroup]="articleForm">
    <ion-item>
      <ion-label stacked  color="primary">
        Title
      </ion-label>
      <ion-input type="text" placeholder="Enter Title"  formControlName="title"></ion-input>
    </ion-item>
    <ion-item>
      <ion-label stacked  color="primary">
        URL
      </ion-label>
      <ion-input type="text" placeholder="Enter URL" formControlName="url"></ion-input>
    </ion-item>
    <ion-item>
      <ion-label stacked  color="primary">
        Categories
      </ion-label>
      <ion-input type="text" placeholder="Add categories"  formControlName="categories"></ion-input>
    </ion-item>
    <ion-item>
      <ion-label color="primary">
        Is a Favorite
      </ion-label>
      <ion-toggle color="positive" checked="false" formControlName="favorite"></ion-toggle>
    </ion-item>
  </form>

</ion-content>
```

![Save](http://res.cloudinary.com/kenatibm/image/upload/b_rgb:ffff00,c_scale,co_rgb:ff0000,e_green:0,h_16,w_16/v1508963561/blog%202017/20171007/save.png) **Save** the file.

Next open the `article-detail.ts` file. Replace the existing code with the following:

```javascript
import { Component } from '@angular/core';
import { IonicPage, NavController, NavParams } from 'ionic-angular';

import { FormGroup, FormBuilder } from '@angular/forms';

import { ArticleModel } from '../../models/article-model';

@IonicPage()
@Component({
  selector: 'page-article-detail',
  templateUrl: 'article-detail.html',
})
export class ArticleDetailPage {
  article: ArticleModel;
  articleForm: FormGroup;
  
  constructor(
    public navCtrl: NavController, 
    public navParams: NavParams, 
    private formBuidler:FormBuilder) {
      this.article = this.navParams.get("article");
      console.log(`==> Article: ${JSON.stringify(this.article)}`);

      this.articleForm = this.formBuidler.group({
        title: [this.article.title],
        categories: [this.article.category],
        url: [this.article.url],
        favorite: [this.article.favorite]
      });
  }

  ionViewDidLoad() {
    console.log('ionViewDidLoad ArticleDetailPage');
  }
}
```

There is a lot going in this file. First there is an import of the `FormGroup` and `FormBuidler` libraries. These libraries are used to bind

![Save](http://res.cloudinary.com/kenatibm/image/upload/b_rgb:ffff00,c_scale,co_rgb:ff0000,e_green:0,h_16,w_16/v1508963561/blog%202017/20171007/save.png) 

**Save** the file.

#### Link the list page to the detail page

Now that the detail page has been created it is time to link the list page to the detail.

Open the `src/pages/article-list/article-list.ts` file. Add the following method:

```
  openArticle(value:ArticleModel){
    this.navCtrl.push('detail', {article: value});
  }
```

The `article-list.ts` file should now look like the following:

```
import { Component } from '@angular/core';
import { IonicPage, NavController, NavParams } from 'ionic-angular';
import { FormControl } from '@angular/forms';

import { ArticleProvider } from '../../providers/article/article';
import { ArticleModel } from '../../models/article-model';

@IonicPage()
@Component({
  selector: 'page-article-list',
  templateUrl: 'article-list.html',
})
export class ArticleListPage {

  allArticles: ArticleModel[];
  statusCode: number;
  searchTerm: string;
  searchControl: FormControl;
  
  constructor(
    public navCtrl: NavController, 
    public navParams: NavParams, 
    private articleProvider: ArticleProvider) {
      this.searchControl = new FormControl();
    }

  ionViewDidLoad() {
    console.log('ionViewDidLoad ArticleListPage');
    this.getAllArticles(0);
  }

  getAllArticles(refresher) {
    this.searchTerm = "";
    this.articleProvider.getAllArticles()
      .subscribe(
        data => {
          this.allArticles = data;
          if(refresher != 0) {
            refresher.complete();
          }
        },
        errorCode => this.statusCode = errorCode
      );
  }

  setFilteredItems() {    
    if(this.searchTerm && this.searchTerm.trim() != '') {
      this.allArticles = this.allArticles.filter(( item ) => {
        console.log(`==> SEARCH: ${item.title} ${this.searchTerm}`);
        return (item.title.toLowerCase().indexOf(this.searchTerm.toLowerCase()) > -1);
      });
    } else {
      this.getAllArticles(0);
    }
  }

  openArticle(value:ArticleModel){
    this.navCtrl.push('detail', {article: value});
  }
}
```

![Save](http://res.cloudinary.com/kenatibm/image/upload/b_rgb:ffff00,c_scale,co_rgb:ff0000,e_green:0,h_16,w_16/v1508963561/blog%202017/20171007/save.png) **Save** the file.

**Next** open the `src/pages/article-list/article-list.html` file. Add a (click) event and point to the openArticle() method:

```html
      <button ion-item *ngFor="let article of allArticles" (click)="openArticle(article)">
```

The file should now look like the following:

```
<ion-header>
  <ion-navbar color="primary">
    <ion-title>
      Articles
    </ion-title>
  </ion-navbar>
</ion-header>
<ion-content>
  <ion-refresher (ionRefresh)="getAllArticles($event)">
    <ion-refresher-content 
      pullingIcon="arrow-dropdown"
      pullingText="Pull to refresh"
      refreshingSpinner="circles"
      refreshingText="Refreshing...">
    </ion-refresher-content>
  </ion-refresher>

  <ion-searchbar 
    [formControl]="searchControl" 
    [(ngModel)]="searchTerm" 
    (ionInput)="setFilteredItems()" 
    (ionCancel)="getAllArticles(0)" 
    [showCancelButton]="shouldShowCancel">
  </ion-searchbar>
  
  <ion-list id="articleList">
        <button ion-item *ngFor="let article of allArticles" (click)="openArticle(article)">
            <ion-icon [name]="article.favorite ? 'star' : 'star-outline'" item-left></ion-icon>
            <h2>{{article.title}}</h2>
            <p>{{article.url}}</p>
        </button>
  </ion-list>
</ion-content>
```

![Save](http://res.cloudinary.com/kenatibm/image/upload/b_rgb:ffff00,c_scale,co_rgb:ff0000,e_green:0,h_16,w_16/v1508963561/blog%202017/20171007/save.png) **Save** the file.


To test, once the save is complete, if the Ionic server is still runing then the app should have been built and the page refreshed.  If not open a terminal or command prompt and start Ionic:

```
ionic serve
```

Got to the list page and press (click) one of the items in the list. This should change the page to the detail page and display the information for the record that was selected. Notice that there is a back Button that was automatically created for the page. Press the Back button to return to the list page.

![Article Detail Page](http://res.cloudinary.com/kenatibm/image/upload/bo_1px_solid_rgb:cccccc,q_auto:eco/v1508972243/blog%202017/20171007/article_detail_page_view.png)

## Adding the In App Browser

The final componet to add is the [In App Browser](https://ionicframework.com/docs/native/in-app-browser/). This will allow the user to vist the url within the app. This requires the installation of an additional plug-in. Open a terminal or command prompt and change directory to the app directory (`~/Projects/articles`), then type the following:

```
ionic cordova plugin add cordova-plugin-inappbrowser
```

It is installed when the following is displayed:

```
> cordova plugin add cordova-plugin-inappbrowser --save
Installing "cordova-plugin-inappbrowser" for android

Installing "cordova-plugin-inappbrowser" for ios

Adding cordova-plugin-inappbrowser to package.json

Saved plugin info for "cordova-plugin-inappbrowser" to config.xml
```

Next install the neccessary node modules by typing:

```
npm install --save @ionic-native/in-app-browser
```

The modules are installed when you see the following:

```
articles@0.0.1 /Users/KenAtIBM/Projects/articles
└── @ionic-native/in-app-browser@4.3.2
```

The next step is to import the Browser library into the `app.module.ts` file. Open the `app.module.ts` file and add the following import statement:

```javascript
import { InAppBrowser } from '@ionic-native/in-app-browser';
```

Also add the `InAppBrowser` to the list of `providers`:

```javascript
  providers: [
  	InAppBrowser,
  	.
  	.
  	.
  ]
```

The updated `app.module.ts` should now look like the following:

```javascript
import { BrowserModule } from '@angular/platform-browser';
import { ErrorHandler, NgModule } from '@angular/core';
import { IonicApp, IonicErrorHandler, IonicModule } from 'ionic-angular';
import { SplashScreen } from '@ionic-native/splash-screen';
import { StatusBar } from '@ionic-native/status-bar';

import { MyApp } from './app.component';
import { ArticleProvider } from '../providers/article/article';
import { HttpModule } from '@angular/http';
import { InAppBrowser } from '@ionic-native/in-app-browser';

@NgModule({
  declarations: [
    MyApp
  ],
  imports: [
    BrowserModule,
    IonicModule.forRoot(MyApp),
    HttpModule
  ],
  bootstrap: [IonicApp],
  entryComponents: [
    MyApp
  ],
  providers: [
    InAppBrowser,
    StatusBar,
    SplashScreen,
    {provide: ErrorHandler, useClass: IonicErrorHandler},
    ArticleProvider
  ]
})
export class AppModule {}
```

![Save](http://res.cloudinary.com/kenatibm/image/upload/b_rgb:ffff00,c_scale,co_rgb:ff0000,e_green:0,h_16,w_16/v1508963561/blog%202017/20171007/save.png) **Save** the file.

#### Update the Article List Page

For the list add the ability to slide one of the items to the left to reveal a button to visit the URL for the selected article. To do this use the [Ionic Sliding Item control](https://ionicframework.com/docs/api/components/item/ItemSliding/).  Open the `src/pages/article-list/article-list.html` file. Add an `<ion-item-sliding>` tag before the `<button ...>` tag in the list.  Also move the `*ngFor` statement from the button to the sliding control.

```html
      <ion-item-sliding *ngFor="let article of allArticles" >
```

Don't forget to add an end tag for the control after the `</button>` tag.

```html
      </ion-item-sliding
```

The updated `article-list.html` file should look like the following:

```html
<ion-header>
  <ion-navbar color="primary">
    <ion-title>
      Articles
    </ion-title>
  </ion-navbar>
</ion-header>
<ion-content>
  <ion-refresher (ionRefresh)="getAllArticles($event)">
    <ion-refresher-content 
      pullingIcon="arrow-dropdown"
      pullingText="Pull to refresh"
      refreshingSpinner="circles"
      refreshingText="Refreshing...">
    </ion-refresher-content>
  </ion-refresher>

  <ion-searchbar 
    [formControl]="searchControl" 
    [(ngModel)]="searchTerm" 
    (ionInput)="setFilteredItems()" 
    (ionCancel)="getAllArticles(0)" 
    [showCancelButton]="shouldShowCancel">
  </ion-searchbar>
  
  <ion-list id="articleList">
      <ion-item-sliding *ngFor="let article of allArticles" >
          <button ion-item (click)="openArticle(article)">
            <ion-icon [name]="article.favorite ? 'star' : 'star-outline'" item-left></ion-icon>
            <h2>{{article.title}}</h2>
            <p>{{article.url}}</p>
        </button>
      </ion-item-sliding>
  </ion-list>
</ion-content>
```

![Save](http://res.cloudinary.com/kenatibm/image/upload/b_rgb:ffff00,c_scale,co_rgb:ff0000,e_green:0,h_16,w_16/v1508963561/blog%202017/20171007/save.png) **Save** the file.

Next open the `src/pages/article-list/article-list.ts` file. Then add an import statement for the `InAppBrowser` and `InAppBrowserOptions`.

```javascript
import { InAppBrowser, InAppBrowserOptions } from '@ionic-native/in-app-browser';
```

Also add an instance variable called `options` and set the `InAppBrowserOptions`.

```javascript
  options : InAppBrowserOptions = {
    location : 'yes',//Or 'no' 
    hidden : 'no', //Or  'yes'
    clearcache : 'yes',
    clearsessioncache : 'yes',
    zoom : 'yes',//Android only ,shows browser zoom controls 
    hardwareback : 'yes',
    mediaPlaybackRequiresUserAction : 'no',
    shouldPauseOnSuspend : 'no', //Android only 
    closebuttoncaption : 'Close', //iOS only
    disallowoverscroll : 'no', //iOS only 
    toolbar : 'yes', //iOS only 
    enableViewportScale : 'no', //iOS only 
    allowInlineMediaPlayback : 'no',//iOS only 
    presentationstyle : 'pagesheet',//iOS only 
    fullscreen : 'yes',//Windows only    
  }; 
```

Add the InAppBrowser to the constructor parameters.

```
,
    private browser: InAppBrowser
```

Lastly add a new method called `visitURL()` that takes one arguement - the URL to view.

```
  visitURL(url: string) {
    console.log(`==> Visit URL: ${url}`);
    let target = "_blank";
    this.browser.create(url, target, this.options);
  }
```

> **Note:** Notice the line `let target = "_blank";`. There are 3 possible targets, they are; 
> 
> 1. "_blank" - Creates a InAppBrowsers component inside the app and displays the url.
> 2. "_system" - Opens the system browser and displays the url.
> 3. "_self" - Opens the cordova InAppBrowsers and displays the url. If this is not defined or added to the app then the system browser is opened.

The updated version of the `article-list.ts` file should look like the following

```javascript
import { Component } from '@angular/core';
import { IonicPage, NavController, NavParams } from 'ionic-angular';
import { FormControl } from '@angular/forms';
import { InAppBrowser, InAppBrowserOptions } from '@ionic-native/in-app-browser';

import { ArticleProvider } from '../../providers/article/article';
import { ArticleModel } from '../../models/article-model';

@IonicPage()
@Component({
  selector: 'page-article-list',
  templateUrl: 'article-list.html',
})
export class ArticleListPage {

  allArticles: ArticleModel[];
  statusCode: number;
  searchTerm: string;
  searchControl: FormControl;

  options : InAppBrowserOptions = {
    location : 'yes',//Or 'no' 
    hidden : 'no', //Or  'yes'
    clearcache : 'yes',
    clearsessioncache : 'yes',
    zoom : 'yes',//Android only ,shows browser zoom controls 
    hardwareback : 'yes',
    mediaPlaybackRequiresUserAction : 'no',
    shouldPauseOnSuspend : 'no', //Android only 
    closebuttoncaption : 'Close', //iOS only
    disallowoverscroll : 'no', //iOS only 
    toolbar : 'yes', //iOS only 
    enableViewportScale : 'no', //iOS only 
    allowInlineMediaPlayback : 'no',//iOS only 
    presentationstyle : 'pagesheet',//iOS only 
    fullscreen : 'yes',//Windows only    
  }; 

  constructor(
    public navCtrl: NavController, 
    public navParams: NavParams, 
    private articleProvider: ArticleProvider,
    private browser: InAppBrowser) {
      this.searchControl = new FormControl();
    }

  ionViewDidLoad() {
    console.log('ionViewDidLoad ArticleListPage');
    this.getAllArticles(0);
  }

  getAllArticles(refresher) {
    this.searchTerm = "";
    this.articleProvider.getAllArticles()
      .subscribe(
        data => {
          this.allArticles = data;
          if(refresher != 0) {
            refresher.complete();
          }
        },
        errorCode => this.statusCode = errorCode
      );
  }

  setFilteredItems() {    
    if(this.searchTerm && this.searchTerm.trim() != '') {
      this.allArticles = this.allArticles.filter(( item ) => {
        console.log(`==> SEARCH: ${item.title} ${this.searchTerm}`);
        return (item.title.toLowerCase().indexOf(this.searchTerm.toLowerCase()) > -1);
      });
    } else {
      this.getAllArticles(0);
    }
  }

  openArticle(value:ArticleModel){
    console.log(JSON.stringify(value));
    this.navCtrl.push('ArticleDetailPage', {article: value});
  }

  visitURL(url: string) {
    console.log(`==> Visit URL: ${url}`);
    let target = "_blank";
    this.browser.create(url, target, this.options);
  }
}
```

![Save](http://res.cloudinary.com/kenatibm/image/upload/b_rgb:ffff00,c_scale,co_rgb:ff0000,e_green:0,h_16,w_16/v1508963561/blog%202017/20171007/save.png) **Save** the file.

To test, once the save is complete, if the Ionic server is still runing then the app should have been built and the page refreshed.  If not open a terminal or command prompt and start Ionic:

```
ionic serve
```

Go to the list, swipe left to reveal the Visit button, then press (click) the View button. This will create a browser view in the app and display the URL that was passed to the browser.

> **Note:** To test on a device simulator or device this will open the device browser and diplay the URL. If you are dying to try this out you will need to have either Xcode (if on macOS) or Android Studio installed and configured with a simulation device. To try on the iOS Simulator, open a terminal session and go to your project directory, then type `ionic cordova emulate ios`. For Android open an terminal session or command prompt and type `ionic cordova emulate android`. 
> 
> **Android Issue:** One thing I noticed with Android is that it does not resolve localhost. Which means that in the article provider the url needs to change to the IP address of the machine, for instance the url may need to be something like http://192.168.0.100:3000/articles replacing the 192.168.0.100 with your machine IP address.

#### Update the Article Detail Page

Next up is to add a button on the detail page that will display the URL similar to the list page. First open the `src/pages/article-detail/article-detail.html`. Below the ending form tag, `</form>`, add the following:

```html
    <button ion-button full outline (click)="visitURL()">
        <ion-icon [name]="'globe-outline'" color="primary" ></ion-icon> Visit {{this.article.title}}
    </button>
```

This will create a button with a title of Visit and the article title. When pressed (clicked) it will call the visitURL() method that is similar to the one created in the article list.

The `article-detail.html` file should look like the following:

```html
<ion-header>
  <ion-navbar color="primary">
    <ion-title>
      Article Details
    </ion-title>
  </ion-navbar>
</ion-header>

<ion-content>
  <form [formGroup]="articleForm">
    <ion-item>
      <ion-label stacked  color="primary">
        Title
      </ion-label>
      <ion-input type="text" placeholder="Enter Title"  formControlName="title"></ion-input>
    </ion-item>
    <ion-item>
      <ion-label stacked  color="primary">
        URL
      </ion-label>
      <ion-input type="text" placeholder="Enter URL" formControlName="url"></ion-input>
    </ion-item>
    <ion-item>
      <ion-label stacked  color="primary">
        Categories
      </ion-label>
      <ion-input type="text" placeholder="Add categories"  formControlName="categories"></ion-input>
    </ion-item>
    <ion-item>
      <ion-label color="primary">
        Is a Favorite
      </ion-label>
      <ion-toggle color="positive" checked="false" formControlName="favorite"></ion-toggle>
    </ion-item>
  </form>

  <button ion-button full outline (click)="visitURL()">
      <ion-icon [name]="'globe-outline'" color="primary" ></ion-icon> Visit {{this.article.title}}
  </button>
</ion-content>
```

![Save](http://res.cloudinary.com/kenatibm/image/upload/b_rgb:ffff00,c_scale,co_rgb:ff0000,e_green:0,h_16,w_16/v1508963561/blog%202017/20171007/save.png) **Save** the file.

Next open the `src/pages/article-detail/article-detail.ts`. Just as was done with the `article-list.ts` the `InAppBrowser` and `InAppBrowserOptions` libraries need to be imported, the `options` variable needs to be created, the `InAppBrowser` needs to be injected into the class via the constructor method, and the `vistURL()` method needs to be created.

First import  the `InAppBrowser` and `InAppBrowserOptions` libraries like so:

```javascript
import { InAppBrowser, InAppBrowserOptions } from '@ionic-native/in-app-browser';
```

Next, create the `options` variable like so:

```javascript
  options : InAppBrowserOptions = {
    location : 'yes',//Or 'no' 
    hidden : 'no', //Or  'yes'
    clearcache : 'yes',
    clearsessioncache : 'yes',
    zoom : 'yes',//Android only ,shows browser zoom controls 
    hardwareback : 'yes',
    mediaPlaybackRequiresUserAction : 'no',
    shouldPauseOnSuspend : 'no', //Android only 
    closebuttoncaption : 'Close', //iOS only
    disallowoverscroll : 'no', //iOS only 
    toolbar : 'yes', //iOS only 
    enableViewportScale : 'no', //iOS only 
    allowInlineMediaPlayback : 'no',//iOS only 
    presentationstyle : 'pagesheet',//iOS only 
    fullscreen : 'yes',//Windows only    
  };
```

Next, inject the `InAppBrowser` into the class via the constructor method

```javascript
,
    private browser: InAppBrowser
```

And finally, add the `visitURL()` method to the class, like so:

```javascript
  visitURL(){
    console.log(`==> Visit URL: ${this.article.url}`);
    let target = "_blank";
    this.browser.create(url, target, this.options);
  }
```

At the end, the `artcile-detail.ts` file should look like the following:

```javascript
import { Component } from '@angular/core';
import { IonicPage, NavController, NavParams } from 'ionic-angular';
import { FormGroup, FormBuilder } from '@angular/forms';
import { InAppBrowser, InAppBrowserOptions } from '@ionic-native/in-app-browser';

import { ArticleModel } from '../../models/article-model';

@IonicPage()
@Component({
  selector: 'page-article-detail',
  templateUrl: 'article-detail.html',
})
export class ArticleDetailPage {
  article: ArticleModel;
  articleForm: FormGroup;

  options : InAppBrowserOptions = {
    location : 'yes',//Or 'no' 
    hidden : 'no', //Or  'yes'
    clearcache : 'yes',
    clearsessioncache : 'yes',
    zoom : 'yes',//Android only ,shows browser zoom controls 
    hardwareback : 'yes',
    mediaPlaybackRequiresUserAction : 'no',
    shouldPauseOnSuspend : 'no', //Android only 
    closebuttoncaption : 'Close', //iOS only
    disallowoverscroll : 'no', //iOS only 
    toolbar : 'yes', //iOS only 
    enableViewportScale : 'no', //iOS only 
    allowInlineMediaPlayback : 'no',//iOS only 
    presentationstyle : 'pagesheet',//iOS only 
    fullscreen : 'yes',//Windows only    
  };
  
  constructor(
    public navCtrl: NavController, 
    public navParams: NavParams, 
    private formBuidler:FormBuilder,
    private browser: InAppBrowser) {
      this.article = this.navParams.get("article");
      console.log(`==> Article: ${JSON.stringify(this.article)}`);

      this.articleForm = this.formBuidler.group({
        title: [this.article.title],
        categories: [this.article.category],
        url: [this.article.url],
        favorite: [this.article.favorite]
      });
  }

  ionViewDidLoad() {
    console.log('ionViewDidLoad ArticleDetailPage');
  }

  visitURL(){
    console.log(`==> Visit URL: ${this.article.url}`);
    let target = "_blank";
    this.browser.create(this.article.url, target, this.options);
  }
}
```

![Save](http://res.cloudinary.com/kenatibm/image/upload/b_rgb:ffff00,c_scale,co_rgb:ff0000,e_green:0,h_16,w_16/v1508963561/blog%202017/20171007/save.png) **Save** the file.

To test, once the save is complete, if the Ionic server is still runing then the app should have been built and the page refreshed.  If not open a terminal or command prompt and start Ionic:

```
ionic serve
```

After the list is displayed, press (click) one of the articles. After the detail page is displayed, press (click) the Visit button. A new page should be opened and the url displayed.

![Article Detail Visit URL](http://res.cloudinary.com/kenatibm/image/upload/bo_1px_solid_rgb:cccccc,q_auto:eco/v1509048376/blog%202017/20171007/article_detail_page_with_visit_url.png)

## Conclusion

In this portion of the tutorial you will learned;

1. How to create a project using Ionic
2. How to create a provider
3. How to create a list and detail page
4. How to display data on the list and detail pages
5. How to search a list of values
6. How to pull to refresh a list of values
7. How to use the InAppBrowser to display a URL


