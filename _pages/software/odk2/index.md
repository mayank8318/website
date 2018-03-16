---
title: ODK 2 Suite & Tools
date: 2018-03-01T00:00:00+00:00
layout: single
permalink: /software/odk2/
sidebar:
  nav: "odk2"
toc: true
---

The **ODK 2.0 Tool Suite** is a new set of ODK tools that will co-exist with the existing ODK 1.0 Tool Suite. It targets advanced users who find themselves limited by the ODK 1.0 data collection workflows. It provides:

- **Fully customizable layout of prompts on the Android device.** The 2.0 tools use HTML, JavaScript, and CSS to specify the layout of nearly all the screens viewed by the data collectors. This enables individuals and organizations with basic web development skills to modify and customize the appearance of their surveys and workflow. At the same time, we retain the easy-to-use spreadsheet-based definition of the survey questions (however, this XLSX Converter mechanism is not cross-compatible with XLSForm).
- **More flexible, user-directed, navigation of a survey.** The 2.0 tools do not impose a strict sequential advancement through a form like ODK Collect; form designers can allow users to traverse a form in any order, yet impose validation of collected data prior to traversing into subsequent steps in a workflow.
- **Improved treatment of repeat-groups.** In the 2.0 tools, we have eliminated the concept of a repeat-group. In its place, we provide prompts that enable you to open and edit other surveys with links back to the originating survey (if desired). These prompts can describe a sub-form (nested) relationship among the surveys (e.g., household and household-member) or they can represent arbitrary relational linkages across your data (e.g., tea-houses and tea-types).
- **Bi-directional synchronization of data across devices.** The ODK 2.0 tools support the collaborative sharing of survey data across devices, as well as the updating and submission of changes to previously-collected data (i.e., follow-up surveys) via a bi-directional synchronization protocol; this contrasts with the unidirectional device-to-server submission pathway of ODK Collect / ODK Aggregate / ODK Briefcase.
- **Data curation and visualization on the device.** ODK Tables gives organizations the ability to investigate and visualize entire datasets directly on the Android devices through graphical and non-graphical displays and through filtered views.
- **Row-level access filters.** The visibility of the data and the ability to edit and/or delete data can be restricted for different users and groups.

**Note:** The ODK 2.0 tool suite is targeted at advanced users who are unable to complete their workflows with the ODK 1.0 tools. If you find that the ODK 1.0 tools meet your needs then there is no reason to switch.
{: .notice--info}

##  List of Tools

Explore our documentation for the ODK 2.0 Tool Suite:

- [**ODK Application Designer:**](https://docs.opendatakit.org/odk2/app-designer-intro/) A design environment for creating, customizing, and previewing your forms, data curation, and visualization applications.
- [**ODK Survey:**](https://docs.opendatakit.org/odk2/survey-intro/) A data collection application based upon HTML, CSS, JavaScript.
- [**ODK Tables:**](https://docs.opendatakit.org/odk2/tables-intro/) A data curation and visualization application running on your mobile device.
- [**ODK Services:**](https://docs.opendatakit.org/odk2/services-intro/) An application for handling database access, file access, and data synchronization services between all the ODK 2.0 applications. It allows you to synchronize data collected by the ODK 2.0 Android tools with a cloud endpoint.
- [**ODK Cloud Endpoints:**](https://docs.opendatakit.org/odk2/cloud-endpoints-intro/) A cloud server to host data and application files, and to support bi-directional data synchronization across disconnected mobile devices.
- [**ODK Suitcase:**](https://docs.opendatakit.org/odk2/suitcase-intro/) A desktop tool for synchronizing data with a cloud endpoint.
