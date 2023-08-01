+++
title = "Mitigating Downtime with Redundancy"
date = 2023-07-31

[taxonomies]
categories = ["News"]
tags = ["Redundancy", "Web Services", "Publishing"]

[extra]
author = "Erik Rose"
+++

High availability refers to an internet service that experiences very little downtime.  Internet availability in a developed society has become a basic utility, analogous to receiving water or power service.  Just as residents expect internet service to be largely uninterrupted, companies providing internet services will often enter into availability contracts, guaranteeing that downtime for their service will not exceed a specific threshold.  The "four nines" of runtime refers to 99.99% uptime, which translates to less than 52 minutes of downtime per year, and this is a standard industry requirement in cloud Service Level Agreements.  Even if our city has not entered in a legally-binding agreement to provide our services with four nines of availability, our residents have grown accustomed to high availability of internet services, to the point that any downtime a city service does experience can have an out-sized negative impact on residents' perception of the service's reliability.  A few poorly-timed incidents of downtime, and residents could begin to avoid using the provided service altogether, because we have failed to meet the user expectation of high availability.

### The GIS Service Pipeline

How do we ensure that city GIS services remain available?  Unfortunately, there are multiple failure points in the GIS service pipeline that can result in service disruption and downtime.  Here we will discuss some strategies that our team uses to mitigate the risks of service disruption at each stage of service delivery.  Let us first consider the minimal elements of a GIS service pipeline {{ figref() }}.

{{ fig_begin(caption = "A basic GIS service pipeline.") }}
<img src=/content/newsfeed/single_pipeline.svg>
{{ fig_end() }}

The ArcGIS Enterprise Server is a running instance owned and operated by the City that hosts all the City's data.  The various different spatial datasets that the City maintains, including water distribution, stormwater, wastewater, transportation and addresses all live on a centralized database running on this server.  Because all members in the organization are viewing and referencing the same shared data on the centralized database, any changes that a single staff member make become instantly visible to the other users.  

Seeing contributions in real time is a strong advantage of using a centralized Enterprise database, and if everyone is running an instance of ArcGIS Pro at their local workstation on the City network, then this setup is sufficient.  But if we want to share the resources on our server with the broader internet world, then we need to publish it as a service.  Publishing GIS data as a service allows others to access it over the web at a set url.  A specific advantage of publishing data from an Enterprise Server is that registered data sources automatically update in close to real time, so the data on the published service stays in sync with its reference data.  Published data services is a prerequisite for browser-based mapping applications, an increasingly popular way of interacting with map data.

Web applications do not reference the published service directly, instead they point to a web map.  The web map is an ArcGIS Item that holds references to published services, determining what data is present and how it is organized.  The only way to view a web map is through some sort of web application, whether that is ArcGIS Online's Map Viewer or a custom web app such as the City Web Viewer.  Web applications control the viewing experience for a given map, and offer a degree of interactivity through widgets, such as the directional finder or drawing tools.

### Redundant Published Services

The first major point of failure in this pipeline is the published service.  What might cause this service to fail?  The Enterprise server could be down, or there could be a localized internet outage.  Is there a way to mitigate this risk?  Part of our licensing agreement with ESRI provides access to ArcGIS Online (AGOL), including an annual allotment of site Credits for purchasing storage and processing services.  Currently, we duplicate every published service available on our local Enterprise server with a corresponding service on ArcGIS Online.  If there is a service interruption of either source, our own server or AGOL, then we can switch services to the other provider and avoid downtime {{figref()}}.

{{ fig_begin(caption = "Redundant published services.") }}
<img src=/content/newsfeed/redundant_server.svg>
{{ fig_end() }}

Hosting services on AGOL can potentially improve load times, because ESRI's servers are hosting the data instead of our own.  However, we do not yet have good telemetry tools in place to benchmark load times, so the evidence is anecdotal.  A definite drawback to AGOL hosting is that we can no longer register our data sources with the service, meaning the data does not automatically sync and update with changes made on our internal server.  Once a week we update the AGOL services by republishing them using the `service_draft.py` and `service_update.py` scripts.  The `service_draft.py` script runs from the Python window of ArcGIS and will tie up the program for about 20 minutes while it prepares service drafts for each of the layers to publish.  The `service_update.py` script runs in the background from the terminal, but may fail to push individual services if any of the processes times out for any reason, and may need resetting before it runs on every service.  Both scripts are at the city repository page under the *scripts* repository.

### Redundant Web Maps

The web map experiences downtime during rebuilds.  We use the `webmap` package from the city repository page to build web maps from published sources.  When these sources change, or when the organization of the layers in the map change, then the map needs to be rebuilt.  The package will first clear the web map of any existing layer data, then replace the empty map with the updated layers.  However, the process of building the new map can take over 20 minutes for large maps like the City Web Viewer.  The build process can also fail for a number of reasons:  the map may reference published content from a third-party provider, such as the PLSS layers maintained by BLM, or the FEMA flood service map.  If the server distributing the third-party content is unavailable for any reason, the build will fail.  If the `webmap` package cannot read all the linked templates, or if any of the internal services are unresponsive, then the build will fail.  Any malformed code created in the latest update could throw runtime errors, causing the build to fail.  Any of these issues could leave you with an empty map object, where the existing layers have been deleted, and the new layers failed to populate the map.

To mitigate downtime during map rebuilds, we use a backup map {{ figref() }}.  The backup is an exact copy of the current map in use by the application.  When we need to update the map, we update the unused backup.  This process could take 20 minutes or more, and we may have to resolve build errors, but since the map is not currently in use by the application, this does not result in downtime for the site.  Once the backup map is fully updated, and we have confirmed that it is functional, we can swap it into the running application for an "instant" update.  Then we can rebuild the map that we swapped out, and this map becomes the new "unused backup" until the next update.

{{ fig_begin(caption = "Backup web map.") }}
<img src=/content/newsfeed/backup_map.svg>
{{ fig_end() }}

### Staged Application Updates

The web application is one of the more stable components of the delivery chain, as we do not have to rebuild it when the target map changes.  If components of the application depend upon properties of the map that have changed, these components will need adjusting or the application may lose some functionality.  For instance, if the application contains filters for a specific layer of the map, and we remove this layer, then the filters will drop as well, because they no longer point to a valid layer.  Some application settings may need adjusting when switching to a backup map: even if the backup is an identical map, some of the widgets, filters and other settings on the application may need to be updated to point at the new map.

The application may also experience flux as you add new features over time or make changes to the user interface.  Staff may request a new feature, or you may just want to try out a new trick from the latest ESRI blog.  The new feature may not work as expected, the new trick might not work at all, or features that were working may stop... how do we experiment with changes to the application without negatively impacting service for the current users?

Our present approach is to use a Beta Version of the application as the development version {{ figref() }}.  All changes and experiments happen on the Beta Version, while the primary version remains stable and continues to deliver services to the user.  After a suitable development period, averaging six weeks, when we are confident that the changes on the Beta Version are stable improvements, then we replace the production version with the Beta Version.  The old production version is retired, the new production version remains stable throughout its service period, and we set up a new Beta Version to support future testing and experimentation.

{{ fig_begin(caption = "Beta Version of Web Application.") }}
<img src=/content/newsfeed/beta_version.svg>
{{ fig_end() }}

### Web Viewer Implementation

The City Web Viewer experiences the highest use among staff and residents, compared to our other web applications.  The Public Viewer serves residents, and has access to most of the same layers as the Staff Viewer, but the staff version includes a few extra layers that are not available to the public.  Using the `webmap` package, we can build the different versions of the web viewer map by passing to the constructor specifying whether the map is public.  We then have a Public Map and Staff Map.  Each map needs a dedicated application pointing at it, so we also have a Public Web Viewer app and a Staff Web Viewer app, with similar configurations, varying slightly depending on the difference in map content between the public and private version.

Since the Public and Staff versions of the web application are so similar, we keep a single Beta Version of the app, and customize the settings depending on the map target when we move the Beta Version into production.  We still keep separate back up maps for each version, because they are built separately.  Both versions of the map use the same published services, even if the staff version includes layers that are not accessible to the public.  Therefore, both maps can rely on either our internal published services or our fallback services on AGOL {{ figref() }}.


{{ fig_begin(caption = "Internal and Public Versions.") }}
<img src=/content/newsfeed/multi_app.svg>
{{ fig_end() }}

Built-in redundancy allows us to have confidence that the services we offer will be consistently available to our users.  However, maintaining redundancies in our production pipeline involves extra effort, producing and maintaining fallback data and services.  When planning for redundancy, consider the potential harm that could result from service downtime.  If the potential for harm is small, the extra levels of redundancy may not be cost-effective to implement and maintain.  When the risk of harm is great, consider these strategies for mitigating negative impacts from downtime.  When service uptime is important, redundancies at each potential failure point in the service pipeline can provide assurance and peace of mind.
