---
title: Help with Image-Based Forms
date: 2010-04-29T22:36:25+00:00
author: system
layout: single
permalink: /software/image-based-forms/
sidebar:
  nav: "software"
toc: true
---

## Images for Localization

Images can be used to localize ODK forms. There are many scripts that Android does not support (for example, many versions do not support Hindi text), but you can work around this using images of text. One way to create these images is to use a desktop paint application like [Paint.net](http://www.getpaint.net/index.html) to create a blank image, type text onto it in whatever language and font you need, and then save it to a file.

## Adding Media to a XLSForm

To add media files to an XLS form create a `media::[media_type]` column with the media’s filename. For example:

<table>
  <colgroup> <col width="63" /> <col width="64" /> <col width="54" /> <col width="133" /> <col width="153" /> <col width="181" /></colgroup> <tr>
    <td>
      survey
    </td>

    <td>
    </td>

    <td>
    </td>

    <td>
    </td>

    <td>
    </td>

    <td>
    </td>
  </tr>

  <tr>
    <td>
    </td>

    <td>
      type
    </td>

    <td>
      name
    </td>

    <td>
      label
    </td>

    <td>
      media::image
    </td>

    <td>
      media::video
    </td>
  </tr>

  <tr>
    <td>
    </td>

    <td>
      note
    </td>

    <td>
      media_example
    </td>

    <td>
      Media example
    </td>

    <td>
      example.jpg
    </td>

    <td>
      example.mp
    </td>
  </tr>
</table>

You can localize media by creating multiple media columns with language name suffixes (i.e. media::image::English)

## Adding media to an XForm

Create an [iText](//opendatakit.org/help/form-design/itext/) element with the media’s filename:

<pre id="xml" class="prettyprint">&lt;text id="NameInHindi"&gt;
   &lt;value form="image"&gt;jr://images/name_in_hindi.png&lt;/value&gt;
&lt;/text&gt;</pre>

Then in the body you can reference it like so:

<pre id="xml" class="prettyprint">&lt;input ref="q1"&gt;
  &lt;label ref="jr:itext('NameInHindi')"/&gt;
&lt;/input&gt;</pre>

There are some examples of multimedia XForms available [in ODK's "sample-forms" repository on GitHub](https://github.com/opendatakit/sample-forms). Take a look at Birds, Miramare, and New Widgets. These same forms are online at <a href="http://opendatakit.appspot.com/">http://opendatakit.appspot.com</a> if you want to try them out on a server.

## Where to Put the Media Files

As detailed in <a href="../help/form-design/itext">help/<wbr>form-design/itext</wbr></a>, the media files (i.e. name\_in\_hindi.png) should be placed in /[external storage directory]/odk/forms/[<wbr>formname]-media. For example, for the form birds.xml, the media would go into /sdcard/odk/forms/birds-media.</wbr>

## Additional Notes

When you design a form, you can have a prompt consist of text, one image, one video, one audio clip

or some combination thereof.

You cannot have one `jr:text` definition in one language that you have defined with an image, and the same `jr:text` definition in another language you have defined only with text. Both prompts must have both images and text. It is fine if those definitions they are blank or empty. [See this item on our issue tracker for more.](https://github.com/opendatakit/opendatakit/issues/563)

If you need to include multiple images on a page, there are two options. You can create a field-list to group multiple prompts together on a single page, or you can use image editing software to combine all your images into a single image.
