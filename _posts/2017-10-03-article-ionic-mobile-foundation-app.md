---
layout: post
title: "Creating an Ionic 3/Mobile Foundation 8 App: The Article App"
date: 2017-10-03 11:59:40
image: 'http://res.cloudinary.com/kenatibm/image/upload/bo_2px_solid_rgb:dddddd/v1506035859/Developer%20Day/blog%202017/2017-09-21.png'
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
* **Previous Article:** [Setup](http://kenatibm.com/article-ionic-mobile-foundation-setup/)

---

In this part of the tutorial I will review the functionality of the app.

## Video

<iframe width="560" height="420" src="http://www.youtube.com/embed/K4CFGNWpQJA?color=white&theme=light"></iframe>

## Screens

### Splash Screen

Not shown in the video is a custom splash screen. You will create this splash screen in the next tutorial.

![Splash Screen](http://res.cloudinary.com/kenatibm/image/upload/v1507076945/splash_ohgung.png)

### List Screen

The list screen displays a list of articles. Tapping an article will take you to the detail information about that article where you can edit the details. Tapping the + (plus) in the toolbar will create a new article.

![List](http://res.cloudinary.com/kenatibm/image/upload/v1507076945/list_hbma6r.png)

### Add (+)/Create Create

If you you tapped the + (plus) in the toolbar on the list page you will see a blank screen to add an new article.

![Add Blank](http://res.cloudinary.com/kenatibm/image/upload/v1507076945/add_ftq33v.png)

![Add Detail](http://res.cloudinary.com/kenatibm/image/upload/v1507076945/add_detail_hjxbrl.png)

### Detail Screen

You will need to enter a title and a valid URL before the Done button is enabled. You can cancel by tapping the Back button. If you want to save/create your new article reference tap the Done button once it is enabled.

![Detail](http://res.cloudinary.com/kenatibm/image/upload/v1507076945/detail_jrg9e0.png)

### Browser Screen

One of the features you will implement is the in-app browser. From the detail screen if you tap the Visit [Web Site] the in app browser will opened with the URL value in the detail screen.

![In App Browser](http://res.cloudinary.com/kenatibm/image/upload/v1507076945/browser_n7hfoy.png)

### List Screen: Search Option

One of the features on the List Screen is the ability to search for items in the list. Tap the search field and begin typing to reduce the items in the list.

![List Search Option](http://res.cloudinary.com/kenatibm/image/upload/v1507076945/search_g69ph2.png)

### List Screen: Pull to Refresh

Another option on the List Screen is to the ability to Pull to Refresh the list. Grab the list and pull down to refresh.

![Pull to Refresh](http://res.cloudinary.com/kenatibm/image/upload/v1507076945/refresh_s3cvs3.png)

### List Screen: Delete List Item

The final option on the List Screen and the **D** in cruD is the ability to delete an item by swipping to the left. This will display option buttons, one being a Delete button and the other a Visit button. The Visit button will open the in app browser and display the URL associated with the item. Tapping the delete button immediately delete the item from the list.

![Delete Item from List](http://res.cloudinary.com/kenatibm/image/upload/v1507076945/delete_iiq1jz.png)

