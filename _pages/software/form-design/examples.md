---
title: Form Design Widget Type Examples
layout: single
permalink: /software/form-design/examples/
date: 2018-03-01T00:00:00+00:00
sidebar:
  nav: "form-design"
toc: true
---

**This page is a reference guide for users who edit the raw XML in ODK forms. If you use the XLSForm form designer, see http://xlsform.org for form design help.**

Here are examples of each prompt type supported by ODK Collect and how each is shown to the user, and the XML snippet that generates the prompt. For full forms, see the [sample forms](https://github.com/opendatakit/sample-forms) repository.

#### Naming your Submission

You can now automatically name each filled-in form in a way that utilizes the data entered into the form. For example, you might use a concatenation of a unique household ID with the respondent name as the name of the filled-in form.

To do this, in the XLS file, add a new instance_name column to your form's settings worksheet. Below that column heading, define the expression that will be used to form the name of the filled-in form. I.e., in this case, you might define:

`concat(${hhid},' - ', ${respondent_name})`

Note that whatever you put in the instance_name column should evaluate to a string; so, for example, "`today()`" alone won't work to name forms using the current date, but "`string(today())`" will work.

This is implemented within the XML as an instanceName field within the meta block. If this value is present and not an empty string (""), it will be used as the name of the filled-in form. Otherwise, the current default naming, based upon the date the form was first saved, will be used.

### Grouping Questions together on One Screen

To group questions together on one screen, wrap the questions in a group with an appearance of "`field-list`".

![Grouping Questions together on One Screen](/assets/images/form-design/FieldList.png){:class="img-responsive"}

```xml
<instance>
  <data xmlns="groupExample">
    <Counts>
      <OPD/>
      <Deliveries/>
      <ANC/>
    </Counts>
  </data>
</instance>

<bind nodeset="/data/Counts/OPD" type="int"/>
<bind nodeset="/data/Counts/Deliveries" type="int"/>
<bind nodeset="/data/Counts/ANC" type="int"/>

<h:body>     
      <group appearance="field-list" ref="/data/Counts">
      <label>Number of cases reported</label>
      <input ref="/data/Counts/OPD">
        <label>OPD last month (#)</label>
      </input>
      <input ref="/data/Counts/Deliveries">
        <label>Deliveries last month (#)</label>
      </input>
      <input ref="/data/Counts/ANC">
        <label>Antenatal last month (#)</label>
      </input>
    </group>
</h:body>
```

### Data Entry Widgets

These provide the various prompts for data entry.

#### Populate a Group of Fields from a 3rd party app

Beginning with ODK Collect 1.4.3, you can invoke a 3rd party app to populate a group of fields within your form. See [External Apps](http://docs.opendatakit.org/launch-apps-from-collect/).

#### String Prompts

These prompts allow a user to type in an arbitrary string. To restrict the size or content of that string, use constraints. Note that ODK Aggregate truncates string values to 256 characters; see [Datastore string length" in Form Design Guidelines](/support/form-design/guidelines/) for how to alter that behavior.

See the "Select One and Select Multiple Prompts" on this page to present a list of fixed choices to the user.

#### String

![String](/assets/images/form-design/string.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_string/>
  </widgets>
</instance>

<bind nodeset="/widgets/my_string" type="string"/>

<h:body>     
  <input ref="my_string">
    <label>string widget</label>
    <hint>can be short or very long</hint>
  </input>
</h:body>
```

Beginning with ODK Collect 1.3, if you want a string field that always displays an edit box with more than one row of text, even if the field's text value could fit on one row, you can specify a rows attribute within the `<input>` tag. I.e.,

```xml
...
<input ref="my_string" rows="5">
  <label>string widget</label>
  <hint>can be short or very long</hint>
</input>
...
```
The above declaration will present a 5-line edit box that will grow larger if necessary but which will never display smaller.

#### String from a 3rd party app

![String from a 3rd party app](/assets/images/form-design/launchStringApp1.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_string/>
  </widgets>
</instance>

<bind nodeset="/widgets/my_string" type="string"/>

<translation lang="English">
  <text id="myStringMsg">
    <value form="short">String App Data</value>
    <value form="long">Launch third party string widget</value>
    <value form="buttonText">Launch StringTool</value>
    <value form="noAppErrorString">StringTool is not installed! Please enter the string manually.</value>
  </text>
</translation>

<h:body>     
  <input ref="my_string" appearance="ex:org.thirdparty.app.ActivityName" >
    <label ref="jr:itext('myStringMsg')"/>
  </input>
</h:body>
```

The intent that is fired is whatever is given after the "ex:" in the appearance tag (in this example, that would be `org.thirdparty.app.ActivityName`. Beginning with ODK Collect 1.4 rev 1033, the current value is passed in the "value" extra to the 3rd party app. The 3rd party app must return a string value under the "value" key of the result intent. I.e., the value is conveyed as follows:

```java
String mAnswer = "response from third party app";
Intent intent = new Intent();
intent.putExtra("value", mAnswer);
setResult(RESULT_OK, intent);
finish();
```

Beginning with ODK Collect 1.4.3, you can pass additional arguments to the 3rd party app. See [External Apps](http://docs.opendatakit.org/launch-apps-from-collect/).

#### String with numeric keypad entry

![String with numeric keypad entry](/assets/images/form-design/StringNumeric.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_string/>
  </widgets>
</instance>

<bind nodeset="/widgets/my_string" type="string"/>

<h:body>     
  <input ref="my_string" appearance="numbers">
    <label>String field that uses only numbers (plus a couple extra)</label>
    <hint>Takes 0-9, -, +, ., space, and comma</hint>
  </input>
</h:body>
```

### Integer Prompts

Integers cannot be greater than 2,147,483,648 or less than 2,147,483,647. If you need to capture a longer integer value, use the **String with numeric keypad entry** prompt type.

#### Integer

![Integer](/assets/images/form-design/int.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_int/>
  </widgets>
</instance>

<bind nodeset="/widgets/my_int" type="int" constraint=". &amp;lt; 10"
  jr:constraintMsg="number must be less than 10"/>

<h:body>     
  <input ref="my_int">
    <label>integer widget</label>
    <hint>try entering a number &amp;gt; 10</hint>
  </input>
</h:body>
```

#### Integer from a 3rd party app

![Integer from a 3rd party app](/assets/images/form-design/LaunchIntegerApp1.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_int/>
  </widgets>
</instance>

<bind nodeset="/widgets/my_int" type="int"/>

<translation lang="English">
  <text id="myIntegerMsg">
    <value form="short">Integer App Data</value>
    <value form="long">Launch third party integer widget</value>
    <value form="buttonText">Launch IntegerTool</value>
    <value form="noAppErrorString">IntegerTool is not installed! Please enter the integer manually.</value>
  </text>
</translation>

<h:body>     
  <input ref="my_int" appearance="ex:org.thirdparty.app.ActivityName" >
    <label ref="jr:itext('myIntegerMsg')"/>
  </input>
</h:body>
```

The intent that is fired is whatever is given after the "ex:" in the appearance tag (in this example, that would be `org.thirdparty.app.ActivityName`. Beginning with ODK Collect 1.4 rev 1033, the current value is passed in the "value" extra to the 3rd party app. The 3rd party app must return an integer value under the "value" key of the result intent. I.e., the value is conveyed as follows:

```java
Integer mAnswer = 2;
Intent intent = new Intent();
intent.putExtra("value", mAnswer);
setResult(RESULT_OK, intent);
finish();
```

Beginning with ODK Collect 1.4.3, you can pass additional arguments to the 3rd party app. See [External Apps](http://docs.opendatakit.org/launch-apps-from-collect/).

### Decimal Prompts

Decimal prompts can represent decimal numbers to about 15 digits of accuracy. If you need to capture a decimal value with higher accuracy, use the **String with numeric keypad entry** prompt type.

#### Decimal

![Decimal](/assets/images/form-design/decimal.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_decimal>18.31</my_decimal>
  </widgets>
</instance>

<bind nodeset="/widgets/my_decimal" type="decimal"
  constraint=". &amp;gt; 10.51 and . &amp;lt; 18.39"
  jr:constraintMsg="number must be between 10.51 and 18.39"/>

<h:body>     
  <input ref="my_decimal">
    <label>decimal widget</label>
    <hint>only numbers &amp;gt; 10.51 and &amp;lt; 18.39</hint>
  </input>
</h:body>
```

#### Decimal from a 3rd party app

![Decimal from a 3rd party app](/assets/images/form-design/LaunchNumericalTool1.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_decimal>18.31</my_decimal>
  </widgets>
</instance>

<bind nodeset="/widgets/my_decimal" type="decimal"/>

<translation lang="English">
  <text id="myDecimalMsg">
    <value form="short">NumericalApp Data</value>
    <value form="long">Launch third party numerical widget</value>
    <value form="buttonText">Launch NumericalTool</value>
    <value form="noAppErrorString">NumericalTool is not installed! Please enter the number manually.</value>
  </text>
</translation>

<h:body>     
  <input ref="my_decimal" appearance="ex:org.thirdparty.app.ActivityName" >
    <label ref="jr:itext('myDecimalMsg')"/>
  </input>
</h:body>
```

The intent that is fired is whatever is given after the "ex:" in the appearance tag (in this example, that would be `org.thirdparty.app.ActivityName`. Beginning with ODK Collect 1.4 rev 1033, the current value is passed in the "value" extra to the 3rd party app. The 3rd party app must return a Double value under the "value" key of the result intent. I.e., the value is conveyed as follows:

```java
Double mAnswer = 3.141592;
Intent intent = new Intent();
intent.putExtra("value", mAnswer);
setResult(RESULT_OK, intent);
finish();
```

Beginning with ODK Collect 1.4.3, you can pass additional arguments to the 3rd party app. See [External Apps](http://docs.opendatakit.org/launch-apps-from-collect/).

#### Bearing (in degrees)

![Bearing (in degrees)](/assets/images/form-design/bearing.png){:class="img-responsive"}

```xml
<instance>
  <widgets id="widgets">
    <my_bearing/>
  </widgets>
</instance>

<bind nodeset="/widgets/my_bearing" type="decimal"/>

<h:body>     
  <input ref="my_bearing" appearance="bearing">
    <label>bearing widget</label>
  </input>
</h:body>
```

When "Record Bearing" is clicked, this then displays the bearing-collection screen:

![Bearing pick](/assets/images/form-design/bearing_pick.png){:class="img-responsive"}

### Date and DateTime Prompts

Year-only, Year-and-month and full date prompt widgets are available. If a Year-and-month widget is used, the recorded date will the be first of the selected month. If a Year-only widget is used, the recorded date will be January 1st of that year.

#### Date

![Date](/assets/images/form-design/date.png){:class="img-responsive"}

On newer Android 4.x devices, this appears as:

![Android 4 Date](/assets/images/form-design/android4-date.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_date>2010-06-15</my_date>
  </widgets>
</instance>

<bind nodeset="/widgets/my_date" type="date" constraint=". &amp;gt;= today()"
  jr:constraintMsg="only future dates allowed"/>

<h:body>     
  <input ref="my_date">
    <label>date widget</label>
    <hint>only future dates allowed</hint>
  </input>
</h:body>
```

#### Date without Calendar

To suppress the calendar on newer Android 4.x devices, use the no-calendar appearance.

![Date without Calendar](/assets/images/form-design/android4-date-no_calendar.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_date>2010-06-15</my_date>
  </widgets>
</instance>

<bind nodeset="/widgets/my_date" type="date" constraint=". &amp;gt;= today()"
  jr:constraintMsg="only future dates allowed"/>

<h:body>     
  <input ref="my_date" appearance="no-calendar" >
    <label>date widget</label>
    <hint>only future dates allowed</hint>
  </input>
</h:body>
```

#### Date displaying only month and year spinner

![Date displaying only month and year spinner](/assets/images/form-design/date-month-year-only.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_date>2012-08-01</my_date>
  </widgets>
</instance>

<bind nodeset="/widgets/my_date" type="date" />

<h:body>     
  <input ref="my_date" appearance="month-year">
    <label>date month-year only</label>
  </input>
</h:body>
```

#### Date displaying only year spinner

![Date displaying only year spinner](/assets/images/form-design/date-year-only.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_date>2012-01-01</my_date>
  </widgets>
</instance>

<bind nodeset="/widgets/my_date" type="date" />

<h:body>     
  <input ref="my_date" appearance="year">
    <label>date year only</label>
  </input>
</h:body>
```

#### Date, time

![Date, time](/assets/images/form-design/datetime.png){:class="img-responsive"}

```xml
<instance>
  <NewWidgets id="NewWidgets">
    <dateTime/>
 </NewWidgets>   
</instance>

<bind nodeset="/NewWidgets/dateTime" type="dateTime"/>
<!-- widget will use am/pm or 24 hour based on the phone's settings. -->
<h:body>       
<input ref="/NewWidgets/dateTime">
  <label>Date and Time Widget</label>
</input>
</h:body>     
```

#### Time

![Time](/assets/images/form-design/time.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_time/>
  </widgets>
</instance>

<bind nodeset="/widgets/my_time" type="time"/>
<!-- widget will use am/pm or 24 hour based on the phone's settings. -->
<h:body>     
  <input ref="my_time">
    <label>time widget</label>
    <hint>testing time</hint>
  </input>
</h:body>
```

### Geo-location Prompts

NOTE: **Device bearing** is a decimal prompt type. See "Bearing Prompt" on this page.

Your Android device can be configured to use either GPS satellites or wireless networks, or both, to determine your location. This configuration is available under Settings / Location and Security / My Location.

ODK Collect uses the selected geo-location method(s) to obtain a location. Users can either immediately accept a lower-accuracy location or wait until the accuracy drops below 5 meters, at which point ODK Collect will automatically accept the location value. See the snippet for how to change this 5m accuracy threshold.

After ODK Collect 1.4.3 (when this functionality was added), when referenced in formulas, the following conversions apply:

- **boolean(.) - Not functional.** There is an underlying library issue that prevents this from working; you must parse the string value and calculate this value. returns true if the geo-location has been captured.
- **number(.) - Not functional.** There is an underlying library issue that prevents this from working; you must parse the string value and calculate this value. returns the accuracy of the geo-location in meters. If the geoPoint has not been captured, this conversion returns 9999999.0 meters (bigger than the radius of the earth).
- **string(.)** - returns the space-separated geo-location or "" if no geo-location has been captured. The values in this string are the latitude, longitude, altitude and accuracy.

#### Location

![Location](/assets/images/form-design/geopoint.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_geopoint/>
  </widgets>
</instance>

<bind nodeset="/widgets/my_geopoint" type="geopoint"/>

<h:body>       
  <input ref="my_geopoint">
    <label>geopoint widget</label>
    <hint>this will get gps location</hint>
  </input>
</h:body>
```

By default, this widget halts the geo-positioning process once the geopoint has an accuracy of 5m or less. To change this, you can supply an "accuracyThreshold" attribute to the `<input>` tag. I.e., to instruct ODK Collect to capture geopoints with accuracies of 1.5m or less, use:

```xml
<h:body>       
  <input ref="my_geopoint" accuracyThreshold="1.5">
    <label>geopoint widget</label>
    <hint>this will get gps location</hint>
  </input>
</h:body>
```

#### Location with map

![Location with map](/assets/images/form-design/geopointmap.png){:class="img-responsive"}

```xml
<instance>
  <NewWidgets id="NewWidgets">
    <locationMap/>
 </NewWidgets>   
</instance>

<bind nodeset="/NewWidgets/locationMap" type="geopoint"/>

<h:body>       
 <input ref="/NewWidgets/locationMap" appearance="maps">
   <label>Geopoint with map Widget</label>
   <hint>Note: this uses DATA and requires a connection</hint>
 </input>
</h:body>                        
```

By default, this widget halts the geo-positioning process once the geopoint has an accuracy of 5m or less. To change this, you can supply an "accuracyThreshold" attribute to the `<input>` tag. I.e., to instruct ODK Collect to capture geopoints with accuracies of 1.5m or less, use:

```xml
<h:body>       
  <input ref="my_geopoint" accuracyThreshold="1.5">
    <label>geopoint widget</label>
    <hint>this will get gps location</hint>
  </input>
</h:body>
```

#### Place and Move Location with map

This widget is only available on Android 2.2 and higher. It requires Google Services (installable via Google Play) and an active internet connection (to access map tiles).

![Place and Move Location with map](/assets/images/form-design/geopointplacementmap.png){:class="img-responsive"}

```xml
<instance>
  <NewWidgets id="NewWidgets">
    <locationMap/>
 </NewWidgets>   
</instance>

<bind nodeset="/NewWidgets/locationMap" type="geopoint"/>

<h:body>       
 <input ref="/NewWidgets/locationMap" appearance="placement-map">
   <label>Geopoint with place and move location on map Widget</label>
   <hint>Note: this uses DATA and requires a connection</hint>
 </input>
</h:body>                        
```

By default, this widget halts the geo-positioning process once the geopoint has an accuracy of 5m or less. To change this, you can supply an "accuracyThreshold" attribute to the `<input>` tag. I.e., to instruct ODK Collect to capture geopoints with accuracies of 1.5m or less, use:

```xml
<h:body>       
  <input ref="my_geopoint" accuracyThreshold="1.5">
    <label>geopoint widget</label>
    <hint>this will get gps location</hint>
  </input>
</h:body>
```

#### Barcode Reader Prompt

Barcode detection relies on a 3rd party app to detect the barcode. Some newer phones provide this capability as part of the camera app. The [Zxing Barcode Scanner](https://play.google.com/store/apps/details?id=com.google.zxing.client.android) is free and works well.

The capabilities of the 3rd party app determine what barcodes or QRCodes can be detected. The Zxing Barcode Scanner will detect both.

![Barcode Reader Prompt](/assets/images/form-design/barcode.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_barcode/>
  </widgets>
</instance>

<bind nodeset="/widgets/my_barcode" type="barcode"/>

<h:body>     
  <input ref="my_barcode">
    <label>barcode widget</label>
    <hint>scans multi-format 1d/2d barcodes</hint>
  </input>
</h:body>
```

#### OpenStreetMap (OSM) OpenMapKit Prompt

Available beginning with ODK Collect 1.4.6

As an alternative to GPS points for location in your survey, you can select an OpenStreetMap feature and associate it with your form instance. This capability is provided through the third-party app [OpenMapKit](https://github.com/AmericanRedCross/OpenMapKit). This prompt uses the [OSM Upload Media Type](/support/form-design/openstreetmap/). With OpenMapKit installed, the Launch OpenMapKit button will launch OpenMapKit where the user selects and tags an OSM feature. That OSM data, with the OSM ID in the file name, is sent back to ODK Collect as a media attachment.

![OpenStreetMap (OSM) OpenMapKit Prompt](/assets/images/form-design/odk_omk.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <osm_building/>
  </widgets>
</instance>

<bind nodeset="/data/osm_building" type="binary"/>

<h:body>
    <upload ref="/data/osm_building" mediatype="osm/*">
      <label>Building</label>
      <hint>Tag attributes about this building.</hint>   
      <tag key="name">
        <label>Name</label>
      </tag>
      <tag key="name:fr">
        <label>Nom en Francais</label>
      </tag>
      <tag key="building_type">
        <label>Building Type</label>
        <item>
            <value>office</value>
            <label>ofisi</label>
        </item>
        <item>
            <value>church</value>
            <label>Kanisa</label>
        </item>
      </tag>
    </upload>
</h:body>
```

### Image Capture, Sketching and Signature Capture Prompts

#### Image capture, select Prompts

Image capture relies on the configuration and capabilities of the device's camera app.

![Image capture, select Prompts](/assets/images/form-design/image.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_image/>
  </widgets>
</instance>

<bind nodeset="/widgets/my_image" type="binary"/>

<h:body>     
  <upload ref="my_image" mediatype="image/*">
    <hint>this will launch the camera</hint>
    <label>image widget</label>
  </upload>
</h:body>
```

#### Image capture, select with annotations

Available beginning with ODK Collect 1.2.1

The dimensions of the captured image will be reduced to fit the device screen prior to annotation. The annotation widget does not support panning or zooming.

![Image capture, select with annotations](/assets/images/form-design/AnnotateWidget.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_image/>
  </widgets>
</instance>

<bind nodeset="/widgets/my_image" type="binary"/>

<h:body>     
  <upload ref="my_image" appearance="annotate" mediatype="image/*">
    <hint>Capture and annotate image</hint>
    <label>image widget</label>
  </upload>
</h:body>
```

#### Freeform drawing

Available beginning with ODK Collect 1.2.1

![Freeform drawing](/assets/images/form-design/DrawingWidget.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_image/>
  </widgets>
</instance>

<bind nodeset="/widgets/my_image" type="binary"/>

<h:body>     
  <upload ref="my_image" appearance="draw" mediatype="image/*">
    <hint>Freeform drawing</hint>
    <label>image widget</label>
  </upload>
</h:body>
```

#### Capture Signature

Available beginning with ODK Collect 1.2.1

![Capture Signature](/assets/images/form-design/Signature.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_image/>
  </widgets>
</instance>

<bind nodeset="/widgets/my_image" type="binary"/>

<h:body>     
  <upload ref="my_image" appearance="signature" mediatype="image/*">
    <hint>Freeform touch signature capture</hint>
    <label>image widget</label>
  </upload>
</h:body>
```

#### Audio capture, select

Audio capture relies on the configuration and capabilities of the device's audio recorder app. On newer 4.x devices and tablets, the supplied audio recorder app may not provide a good user experience when launched from ODK Collect. The [RecForge Lite](https://play.google.com/store/apps/details?id=dje073.android.audiorecorderlite) audio record app is free and may provide a better user experience. If you require longer recordings, a Pro version available.

![Audio capture, select](/assets/images/form-design/audio.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_audio/>
  </widgets>
</instance>

<bind nodeset="/widgets/my_audio" type="binary"/>

<h:body>     
  <upload ref="my_audio" mediatype="audio/*">
    <hint>this will launch the audio recorder</hint>
    <label>audio widget</label>
  </upload>
</h:body>
```

#### Video capture, select

Video capture relies on the configuration and capabilities of the device's camera app.

![Video capture, select](/assets/images/form-design/video.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_video/>
  </widgets>
</instance>

<bind nodeset="/widgets/my_video" type="binary"/>

<h:body>       
  <upload ref="my_video" mediatype="video/*">
    <label>video widget</label>
  </upload>
</h:body>
```

#### Acknowledge

![Acknowledge](/assets/images/form-design/trigger.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_trigger/>
  </widgets>
</instance>

<bind nodeset="/widgets/my_trigger" />

<h:body>     
  <trigger ref="my_trigger">
    <label>acknowledge widget</label>
    <hint>need to push button</hint>
  </trigger>
</h:body>
```

#### Output

![Output](/assets/images/form-design/output.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_output/>
  </widgets>
</instance>

<bind nodeset="/widgets/my_output" type="string" readonly="true()"
  relevant="selected(/widgets/branch, 'n')"/>

<h:body>     
  <input ref="my_output">
    <label>review widget. is your email
      still <output value="/widgets/regex"/>?</label>
    <hint>long hint: there is an upcoming section.</hint>
  </input>
</h:body>
```

### Select One and Select Multiple Prompts</h1>

Select prompts offer the user a selection from among a fixed set of values. For each entry in the list of choices, the designer must specify a string value and one or more translations of the display text to present to the user. ODK Collect records the string value in the field, not the display text. If a select-multiple prompt is used, the string values for the selected choices are stored as space-separated text in that field. Thus, to be interpretable during data analysis, when defining the string values of the choices for a select-multiple field, those string values should not contain any spaces.

There is no way directly within ODK Collect to provide a selection prompt for a changing or growing set of choices. If you need that functionality, you can use the **String from 3rd party app** widget to launch your own application that presents that list of choices to the user and returns the selected value(s) as a string.

#### Select one

![Select one](/assets/images/form-design/select1.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_select1>8</my_select1>
  </widgets>
</instance>

<bind nodeset="/widgets/my_select1" type="select1"/>

<h:body>
  <select1 ref="my_select1">
    <label>select one widget</label>
    <hint>scroll down to see default selection</hint>
    <item>
      <label>option 1</label>
      <value>1</value>
    </item>
    <item>
      <label>option 2</label>
      <value>2</value>
    </item>
    <item>
      <label>option 3</label>
      <value>3</value>
    </item>
    <item>
      <label>option 4</label>
      <value>4</value>
    </item>
    <item>
      <label>option 5</label>
      <value>5</value>
    </item>
    <item>
      <label>option 6</label>
      <value>6</value>
    </item>
    <item>
      <label>option 7</label>
      <value>7</value>
    </item>
    <item>
      <label>option 8</label>
      <value>8</value>
    </item>
  </select1>
</h:body>
```

#### Select one with search

![Select one with search](/assets/images/form-design/select_one_search_320.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_select1>8</my_select1>
  </widgets>
</instance>

<bind nodeset="/widgets/my_select1" type="select1"/>

<h:body>
  <select1 appearance="search"  ref="my_select1">
    <label>select one widget</label>
    <hint>start typing to filter choices</hint>
    <item>
      <label>option 1</label>
      <value>1</value>
    </item>
    <item>
      <label>option 2</label>
      <value>2</value>
    </item>
    <item>
      <label>option 3</label>
      <value>3</value>
    </item>
    <item>
      <label>option 4</label>
      <value>4</value>
    </item>
    <item>
      <label>option 5</label>
      <value>5</value>
    </item>
    <item>
      <label>option 6</label>
      <value>6</value>
    </item>
    <item>
      <label>option 7</label>
      <value>7</value>
    </item>
    <item>
      <label>option 8</label>
      <value>8</value>
    </item>
  </select1>
</h:body>
```

#### Select one with auto-advance

![Select one with auto-advance](/assets/images/form-design/selectadvance.png){:class="img-responsive"}

```xml
<instance>
  <NewWidgets id="NewWidgets">
    <selectadvance/>
 </NewWidgets>   
</instance>

<bind nodeset="/NewWidgets/selectadvance" type="select1"/>

<h:body>       
<select1 appearance="quick" ref="/NewWidgets/selectadvance">
  <label>Select Widget - Auto Advance</label>
  <item>
    <label>Choice 1</label>
    <value>c1</value>
  </item>
  <item>
    <label>Choice 2</label>
    <value>c2</value>
  </item>
  <item>
    <label>Choice 3</label>
    <value>c3</value>
  </item>
  <item>
    <label>Choice 4</label>
    <value>c4</value>
  </item>
</select1>
</h:body>
```

#### Select multi

![Select multi](/assets/images/form-design/select.png){:class="img-responsive"}

```xml
<instance>
  <widgets xmlns="widgets">
    <my_select>a c</my_select>
  </widgets>
</instance>

<bind nodeset="/widgets/my_select" type="select"
  constraint="not(selected(., 'c') and selected(., 'd'))"
  jr:constraintMsg="option c and d cannot be selected together"/>

<h:body>     
  <select ref="my_select">
    <label>select multiple widget</label>
    <hint>don't pick c and d together</hint>
    <item>
      <label>option a</label>
      <value>a</value>
    </item>
    <item>
      <label>option b</label>
      <value>b</value>
    </item>
    <item>
      <label>option c</label>
      <value>c</value>
    </item>
    <item>
      <label>option d</label>
      <value>d</value>
    </item>
  </select>
</h:body>
```

#### Select one spinner

![Select one spinner](/assets/images/form-design/spinner.png){:class="img-responsive"}

```xml
<instance>
  <NewWidgets id="NewWidgets">
    <spinner/>
 </NewWidgets>   
</instance>

<bind nodeset="/NewWidgets/spinner" type="select1"/>

<h:body>       
<select1 appearance="minimal" ref="/NewWidgets/spinner">
  <label>Spinner Widget: Select 1</label>
  <item>
    <label>Choice 1</label>
    <value>c1</value>
  </item>
  <item>
    <label>Choice 2</label>
    <value>c2</value>
  </item>
  <item>
    <label>Choice 3</label>
    <value>c3</value>
  </item>
  <item>
    <label>Choice 4</label>
    <value>c4</value>
  </item>
</select1>
</h:body>
```

#### Select multi spinner

![Select multi spinner](/assets/images/form-design/spinnermulti.png){:class="img-responsive"}

```xml
<instance>
  <NewWidgets id="NewWidgets">
    <spinnermulti/>
 </NewWidgets>   
</instance>

<bind nodeset="/NewWidgets/spinnermulti" type="select"/>

<h:body>       
<select appearance="minimal" ref="/NewWidgets/spinnermulti">
  <label>Spinner Widget: Multi</label>
  <item>
    <label>Choice 1</label>
    <value>c1</value>
  </item>
  <item>
    <label>Choice 2</label>
    <value>c2</value>
  </item>
  <item>
    <label>Choice 3</label>
    <value>c3</value>
  </item>
  <item>
    <label>Choice 4</label>
    <value>c4</value>
  </item>
</select>
</h:body>                          
```

#### Select one grid

![Select one grid](/assets/images/form-design/grid.png){:class="img-responsive"}

```xml
<instance>
  <NewWidgets id="NewWidgets">
    <grid/>
 </NewWidgets>   
</instance>

<bind nodeset="/NewWidgets/grid" type="select1"/>

<h:body>       
<select1 appearance="compact" ref="/NewWidgets/grid">
  <label>Grid Widget</label>
  <hint>Select an Icon</hint>
  <item>
    <label ref="jr:itext('sixChoicesc1')"/>
    <value>c1</value>
  </item>
  <item>
    <label ref="jr:itext('sixChoicesc2')"/>
    <value>c2</value>
  </item>
  <item>
    <label ref="jr:itext('sixChoicesc3')"/>
    <value>c3</value>
  </item>
  <item>
    <label ref="jr:itext('sixChoicesc4')"/>
    <value>c4</value>
  </item>
  <item>
    <label ref="jr:itext('sixChoicesc5')"/>
    <value>c5</value>
  </item>
  <item>
    <label ref="jr:itext('sixChoicesc6')"/>
    <value>c6</value>
  </item>
</select1>
</h:body>
```

To define a grid with a fixed number of columns, specify the number of columns as a '-width' suffix to the 'compact' appearance. I.e., to force 4 columns:

`<select1 appearance="compact-4" ref="/NewWidgets/grid">`

Beginning with ODK Collect 1.3, if you specify a fixed number of columns, the icons will be rescaled to exactly fit the width of the device in its _natural_ orientation. When the device is rotated 90 degrees, the image sizes will remain unchanged, but the number of columns in which they are displayed may change.

Also beginning with ODK Collect 1.3, you can intermingle text with the images, or have an entirely-text-based grid of choices.

#### Select one grid with auto-advance

![Select one grid with auto-advance](/assets/images/form-design/gridauto.png){:class="img-responsive"}

```xml
<instance>
  <NewWidgets id="NewWidgets">
    <gridauto/>
 </NewWidgets>   
</instance>

<bind nodeset="/NewWidgets/grid" type="select1"/>

<h:body>       
<select1 appearance="quickcompact" ref="/NewWidgets/gridauto">
  <label>Grid Widget - Auto Advance</label>
  <hint>Select an Icon</hint>
  <item>
    <label ref="jr:itext('sixChoicesc1')"/>
    <value>c1</value>
  </item>
  <item>
    <label ref="jr:itext('sixChoicesc2')"/>
    <value>c2</value>
  </item>
  <item>
    <label ref="jr:itext('sixChoicesc3')"/>
    <value>c3</value>
  </item>
  <item>
    <label ref="jr:itext('sixChoicesc4')"/>
    <value>c4</value>
  </item>
  <item>
    <label ref="jr:itext('sixChoicesc5')"/>
    <value>c5</value>
  </item>
  <item>
    <label ref="jr:itext('sixChoicesc6')"/>
    <value>c6</value>
  </item>
</select1>
</h:body>                          
```

To define a grid with a fixed number of columns, specify the number of columns as a '-width' suffix to the 'compact' appearance. I.e., to force 4 columns:

`<select1 appearance="compact-4" ref="/NewWidgets/grid">`

Beginning with ODK Collect 1.3, if you specify a fixed number of columns, the icons will be rescaled to exactly fit the width of the device in its _natural_ orientation. When the device is rotated 90 degrees, the image sizes will remain unchanged, but the number of columns in which they are displayed may change.

Also beginning with ODK Collect 1.3, you can intermingle text with the images, or have an entirely-text-based grid of choices.

#### Select multi grid

![Select multi grid](/assets/images/form-design/grid-multi.png){:class="img-responsive"}

```xml
<instance>
  <NewWidgets id="NewWidgets">
    <gridmulti/>
 </NewWidgets>   
</instance>

<bind nodeset="/NewWidgets/gridmulti" type="select1"/>

<h:body>       
<select appearance="compact" ref="/NewWidgets/q5">
    <label>Grid Widget Multi-Select</label>
    <item>
      <label ref="jr:itext('sixChoicesc1')"/>
      <value>c1</value>
    </item>
    <item>
      <label ref="jr:itext('sixChoicesc2')"/>
      <value>c2</value>
    </item>
    <item>
      <label ref="jr:itext('sixChoicesc3')"/>
      <value>c3</value>
    </item>
    <item>
      <label ref="jr:itext('sixChoicesc4')"/>
      <value>c4</value>
    </item>
    <item>
      <label ref="jr:itext('sixChoicesc5')"/>
      <value>c5</value>
    </item>
    <item>
      <label ref="jr:itext('sixChoicesc6')"/>
      <value>c6</value>
    </item>
  </select>
</h:body>
```

To define a grid with a fixed number of columns, specify the number of columns as a '-width' suffix to the 'compact' appearance. I.e., to force 4 columns:

`<select1 appearance="compact-4" ref="/NewWidgets/grid">`

Beginning with ODK Collect 1.3, if you specify a fixed number of columns, the icons will be rescaled to exactly fit the width of the device in its _natural_ orientation. When the device is rotated 90 degrees, the image sizes will remain unchanged, but the number of columns in which they are displayed may change.

Also beginning with ODK Collect 1.3, you can intermingle text with the images, or have an entirely-text-based grid of choices.

#### Select one list

![Select one list](/assets/images/form-design/labeledchoices.png){:class="img-responsive"}

```xml
<instance>
  <NewWidgets id="NewWidgets">
  <listGroup>
    <q8/>
    <q9/>
    <q10/>
    <q11/>
    <q12/>
  </listGroup>
 </NewWidgets>   
</instance>

<bind nodeset="/NewWidgets/listGroup/q8" type="select1"/>
<bind nodeset="/NewWidgets/listGroup/q9" type="select1"/>
<bind nodeset="/NewWidgets/listGroup/q10" type="select1"/>
<bind nodeset="/NewWidgets/listGroup/q11" type="select1"/>
<bind nodeset="/NewWidgets/listGroup/q12" type="select1"/>

<h:body>       
<group appearance="field-list" ref="/NewWidgets/listGroup">
   <label>List Group</label>
   <select1 appearance="label" ref="/NewWidgets/listGroup/q8">
     <label>Labeled Choices</label>
     <item>
       <label>Yes</label>
       <value>yes</value>
     </item>
     <item>
       <label>No</label>
       <value>no</value>
     </item>
   </select1>
   <select1 appearance="list-nolabel" ref="/NewWidgets/listGroup/q9">
     <label>Q1</label>
     <item>
       <label>Yes</label>
       <value>yes</value>
     </item>
     <item>
       <label>No</label>
       <value>no</value>
     </item>
   </select1>
   <select1 appearance="list-nolabel" ref="/NewWidgets/listGroup/q10">
     <label>Question 2</label>
     <item>
       <label>Yes</label>
       <value>yes</value>
     </item>
     <item>
       <label>No</label>
       <value>no</value>
     </item>
   </select1>
   <select1 appearance="list-nolabel" ref="/NewWidgets/listGroup/q11">
     <label>Choice 3</label>
     <item>
       <label>Yes</label>
       <value>yes</value>
     </item>
     <item>
       <label>No</label>
       <value>no</value>
     </item>
   </select1>
   <select1 appearance="list-nolabel" ref="/NewWidgets/listGroup/q12">
     <label>Option 4</label>
     <item>
       <label>Yes</label>
       <value>yes</value>
     </item>
     <item>
       <label>No</label>
       <value>no</value>
     </item>
   </select1>
 </group>
</h:body>
```

#### Select multi list

![Select multi list](/assets/images/form-design/multichoicelist.png){:class="img-responsive"}

```xml
<instance>
  <NewWidgets id="NewWidgets">
  <listGroup>
  <multiListGroup>
    <q13/>
    <q14/>
    <q15/>
  </multiListGroup>
 </NewWidgets>   
</instance>

<bind nodeset="/NewWidgets/multiListGroup/q13" type="select"/>
<bind nodeset="/NewWidgets/multiListGroup/q14" type="select"/>
<bind nodeset="/NewWidgets/multiListGroup/q15" type="select"/>

<h:body>       
<group appearance="field-list" ref="/NewWidgets/multiListGroup">
  <label>Multi List Group</label>
  <select appearance="label" ref="/NewWidgets/multiListGroup/q13">
    <label>Multi Choice List</label>
    <item>
      <label ref="jr:itext('yesnoYes')"/>
      <value>Yes</value>
    </item>
    <item>
      <label ref="jr:itext('yesnoNo')"/>
      <value>No</value>
    </item>
  </select>
  <select appearance="list-nolabel" ref="/NewWidgets/multiListGroup/q14">
    <label>Brian</label>
    <item>
      <label ref="jr:itext('yesnoYes')"/>
      <value>Yes</value>
    </item>
    <item>
      <label ref="jr:itext('yesnoNo')"/>
      <value>No</value>
    </item>
  </select>
  <select appearance="list-nolabel" ref="/NewWidgets/multiListGroup/q15">
    <label>Michael</label>
    <item>
      <label ref="jr:itext('yesnoYes')"/>
      <value>Yes</value>
    </item>
    <item>
      <label ref="jr:itext('yesnoNo')"/>
      <value>No</value>
    </item>
  </select>
</group>
</h:body>  
```

### Printing Widget

Printing is only possible on devices running Android 3.1 or higher.

Printing is available beginning with ODK Collect 1.3; the supplied printing widget uses the ODK Sensors Framework and ODK Zebra Printer Driver to print on Zebra MZ Series printers. We have tested using MZ220 and MZ320 printers.

![Zebra Printer](/assets/images/form-design/zebraPrinterPhotoTrimmed-180x300.png){:class="img-responsive"}

The printing widget emits a label with up to three parts, in order:

1. Numeric barcode
2. QRcode
3. Text output

![Printed Labels](/assets/images/form-design/printed_labels-180x300.png){:class="img-responsive"}

The quantity of data that can be represented in the QRcode is dependent upon the width of the paper on which it is printed (these are the square barcodes that are often used to encode URLs). For the MZ220, the limit is probably around 240 characters.

The printer widget is used whenever a string field supplies 'printer' as the value for its appearance attribute. The value of the string field defines the label to be printed. This will typically be created using a calculate expression.

The label consists of zero or more parts separated by `<br>` (this exact 4-character string). The first part (everything before the first `<br>`) defines the numeric barcode to be printed; if blank, no barcode is printed. The second part defines the QRcode; if blank, no QRcode is printed. The remaining part(s) are the line(s) of text to be printed (if any). Note that the Zebra printer and the printer driver do not recognize or support HTML formatting tags other than this special interpretation of the 4-character `<br>` string.

![Collect Printer](/assets/images/form-design/collect_printer.png){:class="img-responsive"}

```xml
<instance>
  <Demo id="Demo">
    <CustomerName/>
    <printLabel/>
  </Demo>
</instance>

<bind nodeset="/Demo/CustomerName" type="string"/>

<bind nodeset="/Demo/printLabel" type="string" readonly="true()"
    calculate="concat('<br>',/Demo/CustomerName,'<br>Customer Name:<br>',
                       /Demo/CustomerName)"/>

<h:body>
  <input ref="printLabel" appearance="printer">
    <label>Print the customer name as a qrcode and in text label</label>
  </input>
</h:body>
```

As stated above, the printer widget is used whenever a string field has an appearance attribute that begins with '`printer`'. The full form for the appearance attribute is '`printer:intentname`', where the `intentname` identifies the printer driver. If left unspecified, it defaults to the `intentname` of the ODK Zebra Printer Driver. I.e., it is as if the appearance attribute were

`appearance="printer:org.opendatakit.sensors.ZebraPrinter"`

By copying and modifying the ODK Zebra Printer Driver, and specifying the `intentname` for that new driver in your appearance attributes, you can create your own customized label formats without needing to also modify ODK Collect.

### Presentation Options

#### Displaying multiple prompts on a single screen

Multiple prompts can be placed upon the same screen by enclosing them within a group with a "field-list" appearance.

ODK Collect does not recompute the relevance (visibility) of all the questions on a screen as data is entered into those questions. As a result, if you have Q2 relevance (visibility) depending upon an answer to Q1, and both are on the same screen, Q2 will be visible or hidden based upon the initial state of Q1 when the combined screen is shown, and it will never display until you leave and re-enter the screen, at which point the value of Q1 will be re-examined and Q2 will be made visible based upon Q1's (now potentially different) value.

![Displaying multiple prompts on a single screen](/assets/images/form-design/Group.png){:class="img-responsive"}

```xml
<instance>
  <Demo id="Demo">
    <CustomerName/>
    <SSN/>
  </Demo>
</instance>

<bind nodeset="/Demo/CustomerName" type="string"/>
<bind nodeset="/Demo/SSN" type="string"/>

<h:body>
  <group appearance="field-list">
    <input ref="CustomerName">
      <label>Enter customer name</label>
    </input>
    <input ref="SSN">
      <label>Enter customer SSN</label>
    </input>
  </group>
</h:body>
```

#### Autoplay Audio

Upon advancing to a question, the audio clip defined for that prompt can be automatically played by specifying an autoplay attribute with a value of "audio" on the prompt. This attribute can be applied to any widget, but is ignored if the widget is within a field-list (multi-question screen).

```xml
<translation lang="English">
  <text id="customerSsn">
    <value form="short">What is your SSN</value>
    <value form="long">Enter your Social Security Number below</value>
    <value form="audio">jr://audio/askSSN.wav</value>
  </text>
</translation>

<h:body>
  <input ref="CustomerSSN" appearance="numbers" autoplay="audio">
    <label ref="jr:itext('customerSsn')"/>
  </input>
</h:body>
```

#### Autoplay Video

Upon advancing to a question, the video clip defined for that prompt can be automatically played by specifying an autoplay attribute with a value of "video" on the prompt. This attribute can be applied to any widget, but is ignored if the widget is within a field-list (multi-question screen).

```xml
<translation lang="English">
  <text id="customerSsn">
    <value form="short">What is your SSN</value>
    <value form="long">Enter your Social Security Number below</value>
    <value form="video">jr://video/askSSN.3gp</value>
  </text>
</translation>

<h:body>
  <input ref="CustomerSSN" appearance="numbers" autoplay="video">
    <label ref="jr:itext('customerSsn')"/>
  </input>
</h:body>
```

### Preloaded Fields

#### Start and End Timestamps

Form start and end timestamps can be loaded into data elements of your form. The snippet shows two fields receiving the start and end timestamp values, respectively.

```xml
<instance>
  <Demo id="Demo">
    <start/>
    <end/>
  </Demo>
</instance>

<bind nodeset="/Demo/start" type="dateTime"
      jr:preload="timestamp" jr:preloadParams="start"/>
<bind nodeset="/Demo/end" type="dateTime"
      jr:preload="timestamp" jr:preloadParams="end"/>
```

#### Property values

Information about the user and phone can be preloaded into data elements of your form. The snippet shows a field that is preloaded with the Google Account (e-mail) that was configured on ODK Collect's settings page. What value is preloaded is defined by the value of the jr:preloadParams attribute in the bind. The property values beginning with "uri:" prepend a namespace prefix to their values but otherwise return the same value as their non-uri-prefixed counterparts. This can be particularly useful for interpreting device IDs.

<table>
	<tbody>
		<tr>
			<th>jr:preloadParams</th>
			<th>Example</th>
			<th>Notes</th>
		</tr>
		<tr>
			<td>uri:deviceid</td>
			<td>imei:A0006F5E212<br />
			mac:01:23:45:67:89:ab<br />
			android_id:1401111</td>
			<td>Unique identifier of phone. Guaranteed not to be blank. Either the cellular IMEI, WiFi mac address, or Android ID (a unique identifier assigned by the operating system).</td>
		</tr>
		<tr>
			<td>deviceid</td>
			<td>A0006F5E212<br />
			01:23:45:67:89:ab<br />
			1401111</td>
			<td>Unique identifier of phone. Guaranteed not to be blank. Either the cellular IMEI, WiFi mac address, or Android ID (a unique identifier assigned by the operating system).</td>
		</tr>
		<tr>
			<td>uri:email</td>
			<td>mailto:user@your.org</td>
			<td>Google Account configured in ODK Collect settings page</td>
		</tr>
		<tr>
			<td>email</td>
			<td>user@your.org</td>
			<td>Google Account configured in ODK Collect settings page</td>
		</tr>
		<tr>
			<td>uri:username</td>
			<td>username:authuser</td>
			<td>Username configured in ODK Collect settings page. Will be blank if not set. Note that this is not necessarily the username used when submitting the form (since the user can manually specify a different username).</td>
		</tr>
		<tr>
			<td>username</td>
			<td>authuser</td>
			<td>Username configured in ODK Collect settings page. Note that this is not necessarily the username used when submitting the form (since the user can manually specify a different username).</td>
		</tr>
		<tr>
			<td>uri:phonenumber</td>
			<td>tel:12065551212</td>
			<td>Phone number of phone. May be blank (e.g., tablets).</td>
		</tr>
		<tr>
			<td>phonenumber</td>
			<td>12065551212</td>
			<td>Phone number of phone. May be blank (e.g., tablets).</td>
		</tr>
		<tr>
			<td>uri:simserial</td>
			<td>simserial:SD655E212</td>
			<td>SIM serial number of phone. May be blank (e.g., tablets).</td>
		</tr>
		<tr>
			<td>simserial</td>
			<td>SD655E212</td>
			<td>SIM serial number of phone. May be blank (e.g., tablets).</td>
		</tr>
		<tr>
			<td>uri:subscriberid</td>
			<td>imsi:SD655E212</td>
			<td>IMSI of phone. May be blank (e.g., tablets).</td>
		</tr>
		<tr>
			<td>subscriberid</td>
			<td>SD655E212</td>
			<td>IMSI of phone. May be blank (e.g., tablets).</td>
		</tr>
	</tbody>
</table>

```xml
<instance>
  <Demo id="Demo">
    <email/>
  </Demo>
</instance>
<bind nodeset="/Demo/email" type="string"
      jr:preload="property" jr:preloadParams="uri:email"/>
```
