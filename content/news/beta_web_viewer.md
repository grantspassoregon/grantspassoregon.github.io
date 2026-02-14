+++
title = "Beta Testing for New Web Viewer"
date = 2023-07-25

[taxonomies]
categories = ["News"]
tags = ["Info", "News", "Web Viewer"]

[extra]
author = "Erik Rose"
+++

# Beta Web Viewer Open For Testing

Since releasing the Web Viewer in February of 2022, we have received a lot of welcome feedback on how we can improve the user experience.  Although some of the comments have been directed toward how we could improve organization and layout of the map data, the majority of feedback has been about issues with the application interface.  Some commonly-desired features include:

* A button to "restore your previous session".
* Filters for selecting types of content within features.
* A directional navigation widget.
* Tools for selecting multiple features and viewing their attributes in a table.
* Better drawing and measurement tools.

Before we can upgrade the existing Web Viewer to a new version, we need to field test the new app and make sure that it works as intended.  This is where you come in!  Help us test the new Beta version today by clicking on [this link](https://experience.arcgis.com/experience/9c1a9de28a864f59a6fcd5d4dbb5f00c/).

*Why does the Beta version looks so different?* The current Web Viewer uses an ArcGIS Instant App template to provide an application framework.  Instant App templates include a thematic layout and a number of optional app features by default.  Because they are quick and easy to set up, an Instant App template made sense when were starting out, to get a product out quickly and start delivering services to our users right away.  However, these app templates are limited in their ability to incorporate new features and tools.  In order to get the customizability that we needed, we needed to go beyond Instant Apps and target a richer application framework.  Previously, the standard tool for building web apps in ArcGIS was the App Builder.  In recent years, the App Builder has been deprecated in favor of the new Experience Builder.  Experience Builder is based upon the latest version of Java, and is capable of integrating 2D and 3D map layouts, among other improvements.  Eventually, we may decide to start building custom widgets for our apps, in which case we can use Experience Builder Developer Edition or the JavaScript SDK for ArcGIS to create a fully-custom web app.  Custom apps are more difficult to host and maintain, so for this Beta version we are using Experience Builder.

Features that are not implemented in the Beta version, but are on the roadmap to be implemented in the future:

* Web links to public records (Fee in Lieu, Service & Annexation and Deferred Development agreements, AFDs)
* Improved content organization of layers in the map.

Is your preferred feature not on the list?  Do you have changes you would like to see in the next Beta version?  Let us know!  Email us at gis@grantspassoregon.gov.
