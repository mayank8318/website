---
title: Form Design iText Elements
layout: single
permalink: /software/form-design/itext-elements/
date: 2018-03-01T00:00:00+00:00
sidebar:
  nav: "form-design"
toc: true
---

**This page is a reference guide for users who edit the raw XML in ODK forms. If you use the XLSForm form designer, see http://xlsform.org for form design help.**

iText is how we support multiple languages and media in prompt text and/or multiple choices.

## Languages

To implement multiple languages, you need to define an `<itext>` element for each string you want to represent in more than one language.

```xml
<model>
  <itext>
    <translation lang="italian">
      <text id="hello">
        <value>this text would show when italian is selected</value>
      </text>
    </translation>

    <translation lang="english">
      <text id="hello">
        <value>this text would show when english is selected</value>
      </text>
    </translation>
  </itext>
    ...
</model>
```

Then to use those values in the form, simply reference the itext block in the body.

```xml
<input ref="languageQuestion">
   <label ref="jr:itext('hello')"/>
</input>
```

## Media

To add media to prompts or multiple choice answers, use the same syntax for itext, but include the media in the itext definition.

```xml
<text id="robin">
 <value form="long">European robin</value>
 <value form="short">European robin</value>
 <value form="image">jr://images/robin.png</value>
 <value form="audio">jr://audio/european-robin.mp3</value>
</text>
```

The media files should be placed in `/[external storage directory]/odk/forms/[formname]-media`. For example, for the form `birds.xml`, the media would go into `/sdcard/odk/forms/birds-media`.
