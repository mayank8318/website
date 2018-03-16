---
title: Form Design OpenStreetMap Integration
layout: single
permalink: /software/form-design/openstreetmap/
date: 2018-03-01T00:00:00+00:00
sidebar:
  nav: "form-design"
toc: true
---

Support for OpenStreetMap has been added to ODK Collect beginning with ODK Collect 1.4.6.

With the new [OSM Upload Media Type for XForms](https://github.com/AmericanRedCross/OpenMapKit/wiki/XForms-OSM-Upload-Media-Type), we have integrated with the 3rd Party [OpenMapKit](https://github.com/americanredcross/openmapkit) Android app to provide the ability to select and tag OpenStreetMap features. By selecting an OpenStreetMap feature in your form, you have the advantage of referencing the location of the survey to a unique OSM geographic feature instead of a GPS point. A GPS point is not a unique identifier, and user selection of a feature on a map provides specific reference to the place in question.

The basic user flow is that a form is created with an OSM question. The user is then presented with the [OpenMapKit prompt](/support/form-design/examples/#openmapkit-prompt) when filling out a form instance.

![Launch OpenMapKit Prompt](/assets/images/form-design/launch-openmapkit.png){:class="img-responsive"}
**Figure 1: Launch OpenMapKit Prompt**

The user is then presented with a map where she can download or [pre-load](https://github.com/AmericanRedCross/OpenMapKit/wiki/OSM-Data-from-the-Overpass-API) OSM XML data.This data is rendered as an overlay on the map, and points, lines, and polygon renderings of the OSM data can be selected and tagged in the app.

![Selection of a Building Way in OpenMapKit](/assets/images/form-design/2015-08-20-18.49.50.png){:class="img-responsive"}
**Figure 2: Selection of a Building Way in OpenMapKit**

The user can then edit tags associated with the selected OSM feature.

![Editing Tags of OSM Feature](/assets/images/form-design/2015-08-20-19.08.41.png){:class="img-responsive"}
**Figure 3: Editing Tags of OSM Feature**

The specific tags that can be edited, and the type of prompt seen in OpenMapKit is specified in the XForm. This form, for example, has the following upload element with the building material tag specified:

``` xml
<upload mediatype="osm/*" ref="/Dhaka-buildings6/osm_building">
  <label>Please select and tag this building on the map.</label>
  ...
  <tag key="building:material">
    <label>Building Material</label>
    <item>
      <label>Concrete</label>
      <value>concrete</value>
    </item>
    <item>
      <label>Brick</label>
      <value>brick</value>
    </item>
    <item>
      <label>Stone</label>
      <value>stone</value>
    </item>
    ...
  </tag>
  ...
</upload>
```

You can refer to [this XForms Example XML document](https://gist.github.com/hallahan/5aa6bc6909cd413989c5) in which this upload mediatype is specified.

Please refer to the <a href="">[wiki section](https://github.com/AmericanRedCross/OpenMapKit/wiki) of the OpenMapKit [Github repo](https://github.com/AmericanRedCross/OpenMapKit for more details.
