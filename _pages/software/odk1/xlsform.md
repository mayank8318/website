---
title: ODK 1 XLSForm
date: 2010-11-09T21:14:19+00:00
author: Yaw Anokwa
layout: page

permalink: /software/odk1/xlsform/
sidenav: software
---

# ODK 1 XLSForm

<p>XLSForm (formerly XLS2Xform) is a tool to simplify the creation of forms. Forms can be designed with Excel and XLSForm will convert them to XForms that can be used with ODK tools.</p>

<h1>Using the Application</h1>

<ol>
	<li>To design your form read&nbsp;<a href="http://xlsform.org">XLSForm form design</a> help and check out the <a href="/1_0_tools/download/sample_xlsform_xls">sample_xlsform.xls</a>.</li>
	<li>Once your xls form is ready submit it for conversion below.</li>
</ol>

<p><iframe height="240" src="http://23.21.114.69/xlsform/" width="100%"></iframe></p>

<p>If the page above doesn't work, try some of the alternatives below.</p>

<p>&nbsp;</p>

<h1><a name="Alternatives"></a>Other XLSForm converters</h1>

<ul>
	<li>For Windows users, a standalone (non-web-based) version of this tool (without the error report) is also available on our <a href="/1_0_tools/download">downloads page</a>. If you use that tool, you should also download ODK Validate (from the&nbsp;<a href="/1_0_tools/download">downloads page</a>) and run the generated form through that tool to generate an error report.</li>
	<li>Nafundi's <a href="https://gum.co/xlsform-offline">XLSForm Offline</a> is an app for Windows and Mac that can convert and validate forms. It's always available, very fast, and easy to use.</li>
	<li><a href="https://github.com/uw-ictd/pyxform">pyxform</a> is a Python library. It works offline and can be used on the command line to convert forms.</li>
	<li>XLSForm is also available through <a href="https://formhub.org/">Formhub.org</a> and <a href="https://ona.io/">Ona.io</a>. Both services require Internet connection and also make it easy to share converted forms and collected data.</li>
</ul>

<h1><a name="Useful_Notes"></a>Useful Notes</h1>

<ul>
	<li><a href="https://enketo.org/">enketo</a> previews generated from this converter will not include media.</li>
	<li>Forms do not have to be uploaded to <a href="aggregate">Aggregate</a> before they are used. They can be manually added to <a href="collect">Collect</a>. Simply place them in the /odk/forms folder on your Android device’s SD card or in the /sdcard folder.</li>
	<li>For a simpler, more user friendly form designer, try <a href="build">Build</a>. For more powerful form designers, try <a href="http://www.kobotoolbox.org/koboform/">Kobo</a>, or <a href="https://enketo.org/">Enketo</a>. We also have <a href="https://github.com/opendatakit/sample-forms">sample forms</a> and <a href="usage_documentation/form_design">form design documentation</a>. And in particular, <a href="usage_documentation/form_guidelines">design guidelines</a> if you wish to design forms manually.</li>
	<li>When this tool was renamed to XLSForm there were many changes to the syntax. The new version is mostly backwards compatible with the old syntax.</li>
	<li>XLSForm works with ODK Collect version 1.1.7 or later.</li>
</ul>
