---
title: Current Software Projects
date: 2018-03-01T00:00:00+00:00
layout: single
toc: true
permalink: /software/
sidebar:
  nav: "software"
---

**The ODK community currently produces two suites of tools, currently known as "ODK 1" and "ODK 2".** Some users will look at the version number and assume the latest is the greatest, but this is not always the case. For this reason, ODK 2 will be renamed in the near future. _The ODK 2 Suite was designed to co-exist with ODK 1 tools, and does not replace any ODK 1 software._

## ODK 1 Suite: Data Collection Tools

ODK 1 tools are designed to be easier to use, require less setup, and are widely adopted. Tools in the ODK 1 Suite include:

* [**ODK Build:**](http://docs.opendatakit.org/odk-build/) enables users to generate forms using a drag-and-drop form designer. Build is implemented as an HTML5 web-based application and targets the common use case of a simple form.

* [**ODK Collect:**](http://docs.opendatakit.org/collect-intro/) is powerful phone-based replacement for your paper forms. Collect is built on the Android platform and can collect a variety of form data types: text, location, photos, video, audio, and barcodes.

* [**ODK Aggregate:**](http://docs.opendatakit.org/aggregate-intro/) provides a ready to deploy online repository to store, view and export collected data. Aggregate can run on Google&#8217;s reliable and free infrastructure as well as on local servers backed by MySQL and PostgreSQL.

* [**Form Uploader:**](http://docs.opendatakit.org/aggregate-forms/) easily upload a blank form and its media files to ODK Aggregate.

* [**ODK Briefcase:**](http://docs.opendatakit.org/briefcase-guide/) is the best way to transfer data from Collect and Aggregate.

* [**ODK Validate:**](http://docs.opendatakit.org/validate/) ensures that you have a OpenRosa compliant form &#8212; one that will also work with all the ODK tools.

* [**XLSForm:**](http://docs.opendatakit.org/xlsform/) allows XForms to be designed with Excel.

**Source code for all ODK 1 Suite products is available on [GitHub](https://github.com/opendatakit/opendatakit).**

## ODK 2 Suite: Information Management

ODK 2 software is better suited for complex longitudinal studies and requires more technical skills. These tools are meant as next-generation solutions that will co-exist with existing ODK 1 tools. ODK 2 addresses several limitations of the existing ODK 1 Suite's data collection workflows such as:

- Fully customizable layout of prompts on the Android device.
- More flexible, user-directed, navigation of a survey.
- Improved treatment of repeat-groups.
- Bi-directional synchronization of data across devices.
- Data curation and visualization on the device.

Read more about [the ODK 2 Suite](/software/odk2/):

- [**ODK Application Designer:**](https://docs.opendatakit.org/odk2/app-designer-intro/) A design environment for creating, customizing, and previewing your forms, data curation, and visualization applications.
- [**ODK Survey:**](https://docs.opendatakit.org/odk2/survey-intro/) A data collection application based upon HTML, CSS, JavaScript.
- [**ODK Tables:**](https://docs.opendatakit.org/odk2/tables-intro/) A data curation and visualization application running on your mobile device.
- [**ODK Services:**](https://docs.opendatakit.org/odk2/services-intro/) An application for handling database access, file access, and data synchronization services between all the ODK 2.0 applications. It allows you to synchronize data collected by the ODK 2.0 Android tools with a cloud endpoint.
- [**ODK Cloud Endpoints:**](https://docs.opendatakit.org/odk2/cloud-endpoints-intro/) A cloud server to host data and application files, and to support bi-directional data synchronization across disconnected mobile devices.
- [**ODK Suitcase:**](https://docs.opendatakit.org/odk2/suitcase-intro/) A desktop tool for synchronizing data with a cloud endpoint.

## Other Helpful Links

* [The ODK Forum:](https://forum.opendatakit.org) Home of the ODK community. Please search first.
* [Frequently Asked Questions:](http://docs.opendatakit.org/faq/) Look here first before asking for help.
* [Verifying Downloads:](/download/#verifying-download-integrity) How to verify the integrity of files downloaded from this site.
* [ODK Marketplace:](https://forum.opendatakit.org/c/marketplace) A list of ODK implementation companies and opportunities.


## Additional Documentation 

* [Form Design:](/support/form-design/) For manually editing XForms to do more complex things.
* [Image-based Forms:](/support/image-based-forms/) How create image-based forms.
* [Encrypted Forms:](http://docs.opendatakit.org/encrypted-forms/) How to set up and use encrypted forms.
* [Training Guide:](/support/training-guide/) Need help training others on how to use ODK?
