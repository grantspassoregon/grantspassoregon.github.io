+++
title = "Bookmarks in the Web Viewer Beta Version"
date = 2023-07-26

[taxonomies]
categories = ["News"]
tags = ["Web Viewer", "Bookmark", "Beta Version"]

[extra]
author = "Erik Rose"
+++

### Why Do We Need Bookmarks?

With more than a hundred layers of map data available to view on the City Web Viewer, the overlay of information would be overwhelming if they were all visible at once.  Part of the reason we include so many layers is that different departments use different sets of layers for their work, and so although we could set commonly-used layers to start as visible, staff do not agree on the set of layers that should be visible, and their needs change from project to project.  A particular point of frustration with using a browser-based mapping application is that our users will spend time turning on a set of layers related to a specific task, and then have to turn them all on again if they refresh their browser.

This was a common-enough pain point among users that the old version of ESRI's App Builder had a "Restore Your Previous Session" button to set the layer configuration and map extent so that it matched the settings on at the last time of use.  However, the new ESRI Experience Builder does not offer this restore button, instead it has bookmarks.  Bookmarks offer a major improvement over the old "Restore Your Previous Session" button, because you can store multiple configurations as separate bookmarks and switch quickly between them.  Bookmarks also persist more reliably between browser refreshes, while the "Restore Your Previous Session" button had a nasty habit of forgetting where you were last time, forcing you to start over from scratch.

### How Do I Make Bookmarks?

The Bookmarks widget is located along the row of widgets at the right side of the banner at the top of the screen.  The icon looks like a book with a cloth bookmark sticking out:

<img src=/content/newsfeed/bookmark_menu.png alt="Bookmarks Menu" width=400>

To make a new bookmark, open the Bookmarks menu by clicking on the widget, and select the empty thumbnail with the plus sign in it:

<img src=/content/newsfeed/bookmark_new.png alt="New Bookmark" width=300>

Customize the name of the bookmark by clicking in the name field and entering your own text:

<img src=/content/newsfeed/bookmark_name.png alt="Name Bookmark" width=300>

The new bookmark will save the current layer configuration (which layers are visible) and map extent (the location and zoom level) at the time of creation.  When you restart the browser, you can return to these same settings by opening the bookmarks menu and selecting the saved bookmark.  In my case, clicking on the Addresses bookmark will turn on the layers for addresses, parcels, and streets, while moving the map extent back to where it was when I created the bookmark, centered on City Hall:

<img src=/content/newsfeed/bookmark_addresses.png alt="Addresses Bookmark" width=500>

If my next task is to update the water distribution network, this previously involved a lot of clicking on the City Web Viewer, because I would turn on nine different water distribution layers as well as the aerial imagery.  On the new Beta Version, I can set a second bookmark that will set all these layers to "visible" in a single click, and center me over the Water Treatment Plant:

<img src=/content/newsfeed/bookmark_water.png alt="Water Bookmark" width=500>

Being able to save workspace state in the Web Viewer app has been our most commonly-requested feature, and we are hopeful that the new Bookmark widget will help streamline the experience for our users and make the Web Viewer a more viable and productive tool for our staff.  If you would like to help test out this feature on the new Beta Version, feel free to give it a try at [this link](https://experience.arcgis.com/experience/9c1a9de28a864f59a6fcd5d4dbb5f00c), and do not forget to let us know what you think!
