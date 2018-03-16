---
title: ODK 1 Sensors
date: 2010-11-09T21:14:19+00:00
author: Yaw Anokwa
layout: page

permalink: /software/odk1/sensors/
sidenav: software
---

# ODK 1 Sensors

**Not released for production &#8211; currently in ALPHA stage of development**

The ODK Sensors framework simplifies the development of sensor-based mobile applications by creating a common abstraction that enables all sensors to be accessed through a unified sensing interface. This single interface exposes external sensors (e.g. USB, Bluetooth) as well as Android’s built-in sensors through a common interface.  Connecting an external sensor requires a sensor driver that transforms the sensed data into a format that is easily usable by applications. The sensors framework handles threading and buffering, allowing sensor driver developers to focus on writing minimal pieces of sensor-specific code. By creating a sensor framework with separate sensor driver components we hope to enable an ecosystem of sharable and reusable sensor drivers.

Currently, the ODK Sensors Framework supports sensors over the USB and Bluetooth communication channels as well as Android&#8217;s built-in sensors.

## Installation

  1. Please read all the instructions and notes before beginning.
  2. You will need an Android 3.1 or higher device (like the [Google Nexus 4](https://en.wikipedia.org/wiki/Nexus_4)) to install Sensors.

### Downloading from Google Play

  1. From your device&#8217;s application drawer, choose the Play Store.
  2. Search for &#8220;ODK&#8221; choose &#8220;ODK Sensors Framework&#8221; from &#8220;Open Data Kit&#8221;.
  3. Select that result and click the Install button. Click OK after viewing the security settings.

### Downloading from Web

  1. From your device&#8217;s application drawer, choose Settings, then Applications. Make sure Unknown sources is checked.
  2. Return to the application drawer and choose Browser. Navigate to [Download](/download/) and download &#8220;ODK Sensors Framework vN.N&#8230;apk&#8221;
  3. In the download window, you will see &#8220;ODK Sensors Framework vN.N&#8230;apk&#8221;. Select it to download the file. On older devices, the APK will automatically install after you approve the security settings. On newer devices, you must go to the download list, rename the file to restore the .apk extension (the extension will have been renamed to .man during the download process), then click on it to install it.

## Using ODK Sensors

In order to use ODK Sensors with a physical sensor you will need to install the appropriate driver for that sensor. Please see the [Zebra Printer driver](/software/odk1/sensors/zebra-printer-driver/) for an example of a driver that allows applications to print text, barcodes and QR codes using a Bluetooth-enabled printer. The very first time your application accesses a physical sensor via ODK Sensors, the framework guides you through the process of discovering the sensor and associating it with a driver. Please see the **Configuring the ODK Zebra Printer Driver** section of the [Zebra Printer driver](/software/odk1/sensors/zebra-printer-driver/) for an example.

Please see the video below for an application that leverages ODK Sensors to safely pasteurize human breast milk. This application communicates with a Bluetooth-enabled temperature sensor to guide users through the pasteurization process. When pasteurization completes the application allows users to print a report and labels for pasteurized milk bottles.

<p><iframe frameborder="0" height="315" src="https://www.youtube.com/embed/yEXqJyzK0nM" width="560"></iframe></p>
