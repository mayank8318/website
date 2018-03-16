---
title: Form Design Guidelines
layout: single
permalink: /software/form-design/guidelines/
date: 2018-03-01T00:00:00+00:00
sidebar:
  nav: "form-design"
toc: true
---

**This page is a reference guide for users who edit the raw XML in ODK forms. If you use the XLSForm form designer, see http://xlsform.org for form design help.**

Gathered below are a set of guidelines for creating your forms. These range from naming suggestions to feature and performance considerations.

## Form ID Guidelines

Open Data Kit depends upon the presence of either the "id" attribute (preferred) or the "xmlns" (deprecated) on the tag within the Xform's `<instance>` tag to uniquely identify the form. Filled-in forms, when finalized by ODK Collect, contain this "id" attribute. When these are submitted to the server (e.g., ODK Aggregate), it extracts the form id and retrieves the corresponding, previously-uploaded, form definition. Using that form definition, the server can then extract the data values from the submission and store them in the appropriate data tables.

Within ODK Aggregate, the Form ID is used in the persistence layer as a prefix for the names of the tables into which your form data is stored. Most persistence mechanisms, and particularly databases like MySQL, restrict the lengths of their column and table names to fewer than 64 characters. For this reason, it is recommended:

- The form ID should be short (ideally < 10 characters).
- The form ID should be unique within your organization.
- The form ID must not contain any spaces or punctuation characters.
- The form ID should contain only alphanumeric characters and the characters `_` and `-`.
- The form ID should start with a letter.
- It may be useful to add a revision designation to the form ID (e.g, "medinfo-01") to aid in tracking major revisions to your forms.
- A separate *version* setting is used for revisions that do not change the data being collected or their data types. These 'minor' revisions include adding language translations, correcting spelling errors within the text, changing external dataset files, and updating multi-media prompts. E.g., changing the media files used in audio, image or video labels (prompts). Using the version setting enables form definitions to be enhanced mid-survey while allowing all of the older and newer submissions to be stored in the same data table on the ODK Aggregate server. The version of the form definition used is retained in the meta-data of each individual submission so that it is available during data analysis.

**NOTE:** Underscores and dashes may limit or complicate the publish-ability of the form to other systems such as Google Spreadsheet or Google Fusion Tables. If you want to use these, please verify that the data can be published to those systems.

**NOTE: Once a form is uploaded to ODK Aggregate, the number of questions or the type of question cannot be changed.** You either have to delete the form from the datastore (deleting all of its submissions) or change the id or xmlns attribute to re-upload the form (in which case it will be treated as an entirely different form and can co-exist with the original). This is by design — it prevents you from changing the format of the data mid-data-collection (which could confound ODK Aggregate's ability to extract the data values submitted using the earlier versions of the form or create database problems). But, as noted above, other changes to the form definition are allowed through the use of the version setting.

These two values that identify a form are specified on the XLSForm spreadsheet's settings tab:

- **form_id** -- must be changed when the data model changes (when you add or remove a prompt, or change a prompt from a string to an integer or decimal or multiple-choice value).
- **version** -- must be a small 10-digit-or-less numeric string. We recommend using strings of the form: 'yyyymmddrr' e.g., 2015012901 (the 1st revision on January 29, 2015). Revised form definitions must have a version string that compares lexically (alphabetically) greater than the current form definition. I.e., ODK Aggregate does not accept changes to a form definition unless the version string is different and lexically (alphabetically) greater than the version string of the existing form definition (and the version string must be a 10-digit-or-less integer).

As mentioned above, if you leave the form_id unchanged, and change the version, then you can upload the new form XML to ODK Aggregate. The new form will replace the old one on ODK Aggregate (you will no longer be able to download the older form), and the new and old form submissions will be submitted into the same submissions table. The version of the form used when the survey was finalized is available as metadata on each submission.

## Group and Field Name Guidelines

Answers to your survey questions are identified by their field names within your form. In ODK Build, the Data Name property specifies the field name. In an XLSForm spreadsheet, the name column specifies the field name. Question groupings also have names, and these guidelines also apply to their names.

Field names appear as the column headers in the *Submissions* tab in ODK Aggregate. If they are nested within a group, the group name and field name (space-separated) appear as the column header. In the exported CSV file, the group name and field name are concatenated with colon separators (:). Because group names and field names are displayed to the data analyst and/or end user, they should be meaningful.

The structure of the data you send is defined in the `<instance/>` section of the XForm. An example, with field names: name, age and date, is shown here:

```xml
<model>
	<instance>
		<data id="sampleForm">
			<name/>
			<age/>
			<date/>
		</data>
	</instance>
	...
</model>
```

An example transmission from ODK Collect of a filled-in form with this structure is shown below (new-lines inserted for readability):

```xml
<?xml version='1.0' ?>
<data id="sampleForm">
<name>John Smith</name>
<age>23</age>
<date>2010-09-17T22:16:16.536</date>
</data>
```

As you can see, even with short field names, around 50% of the size of the message is consumed by the field names. The more grouped and deeply nested your form is, the more space will be consumed by the names of these groups and their nesting. If you are gathering text-only data, and pay for the amount of data you transmit, you should strive to use the shortest possible meaningful field names. But, again, for downstream usability, we strongly recommend meaningful names (e.g., "age" is easier to comprehend than "q2").

All these message size concerns are insignificant if you are transmitting captured audio, image, or video clips. In that case, the size of the captured images, audio or video will be several orders of magnitude greater than the size of any textual form data you might collect.

Finally, within ODK Aggregate, the field and group names are mapped to the specific columns or tables in which the data for those fields (or groups of nested fields) are stored. Most persistence mechanisms, and particularly databases like MySQL, restrict the lengths of their column and table names to fewer than 64 characters. Aggregate will compact your field names to fit within those limits and use those compacted names as the column and table names in the datastore. The compacted names of deeply nested fields or fields with long field names may be awkwardly cryptic if you are accessing the datastore (e.g., MySQL) directly.

Compacted names are formed by prefixing the name(s) of the groups in which the field is nested to the field's name, each separated by a `_` character. All lower case characters are then capitalized and an `_` character is inserted at word breaks; non-alphanumeric characters are also replaced with `_` characters. The group prefix is then compacted to consume no more than 1/3 of the column name allowed by the datastore; the field name is compacted to fit the remaining space.

Thus, thisFormField and this-form-field will both become THIS_FORM_FIELD, as would a field named Field nested within a thisForm group. Any overlaps of the resulting column names within a single database table are prevented through additional processing steps.

In light of these processing steps, it is recommended that field names:

- Be short (ideally < 30 characters).
- Must be unique within their enclosing group within the form (this is required by Xml and Javarosa).
- Cannot contain any spaces.
- Should contain only alphanumeric characters and the characters `_` and `-`.
- Should start with a letter.
- Should all consistently follow either the camel-case convention (e.g., thisFormField) with leading capitals denoting word breaks within the field name, or use either the `_` or `-` characters to mark word breaks (e.g., this-form-field).
- Should not have two or more fields that are distinguished only by either their capitalization, use of dashes, or use of underscores. E.g., a form that contains two or more of these field names will be confusing: `thisFormField`, `this-form-field`, `thisformfield` or `this_formField`.

**NOTE:** Underscores and dashes within the field name (*not* the compacted name) may limit or complicate the publish-ability of the form to other systems such as Google Spreadsheet or Google Fusion Tables. If you want to use them, please verify that the data can be published to those systems.

## Select Values

The underlying values defined with `<value>` tag for select clauses should follow the same naming as the field names, above. In particular, these values should not contain embedded spaces, as the parsing at the server will split the strings at the spaces, causing "my value" to be stored on the server as two selection values "my" and "value".

## Forms with Images/Audio/Video included in the prompts

You can now use images, audio, and video (in any combination) in addition to or in place of text in questions and in multiple choice answers. To use media we have taken advantage of javarosa's itext framework. Like text, a media file can be different for each language specified in the form.

To define your media, declare one or more `<text id>` fields in `<itext>`. Example:

```xml
<itext>
  <translation lang="English" default="">
    <text id="my_media">
      <value form="long">This is a question with an not-clickable image</value>
      <value form="short">audio and image</value>
      <value form="image">jr://images/test.gif</value>
    </text>
  </translation>
</itext>
```

Then, in the `<body>` reference the text id as the `<label>` in either a question or an element in a select1:

```xml
<input ref="image_question">
    <label ref="jr:itext('my_media')"/>
</input>
```

or

```xml
<select1 ref="select_question">
  <label> Select one with images and audio </label>
  <item>
    <label ref="jr:itext('my_media')" />
    <value>a</value>
  </item>
</select1>
```

## Itext Value Tag Types

The possible choices for the form attribute of the itext `<value>` tag are:

- `long`,
- `short`,
- `image`,
- `audio`,
- `video`, and
- `big-image`.

By default, itext "image" values are not clickable. However, if you also include a "big-image", the image displayed by "image" will be clickable and will display a pannable, zoomable view of the file specified by "big-image". You can return to your form after opening a "big-image" by hitting the phone's "back" button. Specifying "big-image" alone has no effect, you must always include "image".

Files referenced by "image" and "big-image" may be the same; however, to improve the user experience, we highly recommend creating smaller thumbnail images to be referenced by "image" (images will display faster if they do not need to be dramatically scaled down).

Audio files will play until complete, or until the user swipes to another prompt.

Video plays in a separate player allowing play, stop, and a scroll bar to jump to a specific spot. Once the video finishes playing, the user will be automatically returned to the form. Users may also return at any time by hitting the phone's "back" button.

## Usable Image, Audio and Video Formats

The formats listed are **what we've tested and verified as working.** There may be more formats that are supported by Android.

<table>
	<tbody>
		<tr>
			<th>&nbsp;</th>
			<th>Supported Format</th>
		</tr>
		<tr>
			<td>Image files:</td>
			<td>jpg, jpeg, gif, png</td>
		</tr>
		<tr>
			<td>Audio files:</td>
			<td>mp3, wav</td>
		</tr>
		<tr>
			<td>Video files:</td>
			<td>3gp, mp4</td>
		</tr>
	</tbody>
</table>

For each form, media needs to be put on the SD card into:

`/sdcard/odk/forms/{formname}-media/`

Media needs to be specified in the xform as:

`jr://{type}/mediafile`

... where type is one of "images", "audio", or "video".

## Stricter Form Syntax - ODK Aggregate 1.x

Form syntax is checked more strictly in ODK Aggregate 1.x than in the earlier ODK Aggregate 0.9.x software. This causes uploads of forms to fail with a 400 error that would otherwise upload successfully in 0.9.x. The stricter syntax is in three areas:

(1) ODK Aggregate 1.x requires that if you use an xmlns attribute to define the form id, that it be in the form of a URI.

Often, the example forms have:

{% highlight xml %}
...
<model>
   <instance>
       <blah xmlns="myformid">
     ...
{% endhighlight %}

In this case, uploading the form will fail. You can either change the "myformid" to something like "http://your.org/myformId" (or anything else that looks like "http://domain.name/..."), or you can omit the xmlns and use an id attribute. If you have both an xmlns and an id attribute, the id attribute will be used. Changing the xmlns to id is the easiest fix:

{% highlight xml %}
<model>
  <instance>
     <blah id="myformid">
...
{% endhighlight %}

This change makes it easier to use xml parsing tools that understand and respect xmlns namespaces. It moves the forms closer to well-formed XML and the XForms spec. It also supports eventually validating the form declaration syntax with an xsd linked to the xmlns, should anyone want to go down that path.

(2) ODK Aggregate 1.x is much pickier about having `<bind>` entries defining the data types of each field in your form. These are easy to overlook in calculated fields, and in fields you have in your form but are not using. The eIMCI example form requires at least two dozen changes to bring it into compliance for ODK Aggregate 1.x. Most of those are because the calculated fields don't declare types.

The stricter `<bind>` handling is needed so that ODK Aggregate 1.x can create database tables with appropriate column types. Rather than let you omit the types and have ODK Aggregate assume it is a string, it forces you to declare the type. The one caveat to be aware of is that multiple-select fields are always treated as space-separated string values.

(3) ODK Aggregate 1.x now supports `submission` tags. If you have a large survey and only need to submit a summary portion of the form to ODK Aggregate, you can now have:

`<submission ref="/data/subset" method="form-data-post" action="http://yourapp.appspot.com/submission" />`

And this will submit the /data/subset portion of your form to the server, rather than the whole form. For this to work, the /data/subset must have an id or xmlns attribute that matches the form id at the top of the data element:

{% highlight xml %}
<model>
    <instance>
        <data id="myForm">
           ...
           <subset id="myForm">
         ...
{% endhighlight %}

If the id's don't match, you won't be able to upload the form. NOTE: ODK Collect 1.1.7 recognizes the submission tag, but not the ref attribute. Earlier versions of ODK Collect don't recognize the submission tag.

## Datastore String Length

In ODK Aggregate 1.x, you can supply an attribute to the `<bind />` to specify the maximum number of characters used to store a string field; by default, the datastore layer limits strings to 255 characters or less. If a submission has data beyond this length, it is silently truncated upon submission.

Specifying a value less than 255 can significantly improve the storage efficiency of the database layer. You can also specify a value greater than 255, up to a maximum of about 16000 UTF-8 characters. The higher you set this value, the worse the storage efficiency within the datastore.

To set the string length:

Step 1: In the header of the form definition, add a xmlns alias for odk (shown added as the last xmlns alias at the bottom of the `<h:html>` tag):

```xml
<?xml version="1.0"?>
<h:html xmlns="http://www.w3.org/2002/xforms"
        xmlns:h="http://www.w3.org/1999/xhtml"
        xmlns:ev="http://www.w3.org/2001/xml-events"
        xmlns:xsd="http://www.w3.org/2001/XMLSchema"
        xmlns:jr="http://openrosa.org/javarosa"
        xmlns:odk="http://www.opendatakit.org/xforms"
        >
    <h:head>
     ...
```

Then, in the bind, you can define an `odk:length` attribute to specify the length of a string field. Length can be specified for barcode, select1 and string fields. Multi-selects (select) fields have a 255 character maximum length for each selection value (and selection values must not contain whitespace); there are no limits to the number of choices that may be selected within a multi-select.

`<bind nodeset="/nm/repeat_observation/notes" type="string" odk:length="600"/>`

### XLSForm support for odk:length

This is partially supported in XLSForm. In your survey sheet, create a column with this heading:

`bind::odk-length`

And, within that survey sheet, specify the number of characters needed for each text field that can hold more than 250 characters. e.g.,

`600`

**NOTE** Text fields should not hold more than about 16,000 characters. If you require text strings of that size or larger, you should consider using file attachments. MySQL systems cannot hold more than about 16,000 characters.

When you generate the form, on the XLSForm tool on the ODK site, you will see a warning:

```
ODK Validate Warnings:
XForm Parse Warning: Warning: 1 Unrecognized attributes found in Element [bind] and will be ignored: [odk-length] Location:

    Problem found at nodeset: /html/head/model/bind
    With element <bind nodeset="/choice/hh/name" odk-length="600" required="true()" type="string"/>

    Problem found at nodeset: /html/head/model/bind
    With element <bind nodeset="/choice/hh/name" odk-length="600" required="true()" type="string"/>
```

**This IS EXPECTED.**

Download the form.

Edit the form in a text editor.

- At the very top of the form, add: `xmlns:odk="http://www.opendatakit.org/xforms"` to the `<h:html ...>` line (2nd line in file) in a manner similar to the other xmlns directives in that line.
- Search-and-replace `odk-length` with `odk:length`.

Save your changes.

Download and run ODK Validate on this file. You should get warnings similar to the ones reported by the XLSForm tool, but with the bind line printing with 'length' and not 'odk:length' or 'odk-length'.

Upload the form to your ODK Aggregate server.

Note that the field-length specification is ignored if this is an updated version of an existing form. The field-length specification is only used the first time a form is uploaded to ODK Aggregate. After that, all changes to this setting in subsequent versions are ignored because the table structures and storage have already been allocated.
