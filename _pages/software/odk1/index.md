---
title: ODK 1 Suite & Tools
date: 2018-03-01T00:00:00+00:00
layout: single
permalink: /software/odk1/
sidebar:
  nav: "odk1"
---

**This page has been deprecated and is out of date.** For up-to-date information on using Open Data Kit, see the [Getting Started Guide](http://docs.opendatakit.org/getting-started/) in the new [ODK Documentation Hub](http://docs.opendatakit.org/).
{: .notice--danger}

Specifically, check out documentation about each of the main ODK 1 Suite tools, including:

- [Collect](http://docs.opendatakit.org/collect-intro/), a phone-based replacement for your paper forms.
- [Aggregate](http://docs.opendatakit.org/aggregate-intro/), a repository to store, view and export collected data.
- [Briefcase](http://docs.opendatakit.org/briefcase-guide/), to transfer data from Collect and Aggregate.
- [Build](http://docs.opendatakit.org/odk-build/), a drag-and-drop form designer.


Our earlier information remains below.

<hr>

<p>To use ODK 1.x, you need to do at least three things -- design a form, setup a server, and connect the device to that server. Once those three things are done, you'll be ready to start data collection.</p>

<p>You'll need three tools:</p>

<ul>
	<li><a href="/software/odk1/build">Build</a> or <a href="/software/odk1/xlsform">XLSForm</a> -- to design your survey form.</li>
	<li><a href="/software/odk1/collect">Collect</a> -- running on an Android device to download and fill-in the survey.</li>
	<li><a href="/software/odk1/aggregate">Aggregate</a> -- for hosting the survey form and gathering the survey results. Alternatively, <a href="/software/odk1/briefcase">Briefcase</a> can be used to gather the survey results (but you'll need to manually place the survey form onto the Android device).</li>
</ul>

<p>If any of this sounds complicated, we promise it's not! As one user said, "<em>the instructions on the ODK site for doing this were easy-breezy to follow</em>." If you run into problems, ask questions on the <a href="https://forum.opendatakit.org/">community forum</a>.</p>

<p>Below is a <a href="https://www.youtube.com/watch?v=lo8LaFFSkV8">demo video</a> of Collect, our Android-based data collection client. Watch it, then start with the instructions for <a href="/software/odk1/collect">Collect</a>, then try <a href="/software/odk1/build">Build</a> and <a href="/software/odk1/aggregate">Aggregate</a>. For longer forms and more complicated branching, we recommend using <a href="/software/odk1/xlsform">XLSForm</a> to design your form.</p>

<p><iframe frameborder="0" height="328" src="https://www.youtube.com/embed/HqqUdfz9Uyc?hd=1" width="530"></iframe></p>

<p>Below are the released and supported ODK 1.0 projects.</p>

<ul>
	<li><a href="/software/odk1/build">Build</a> - ODK Build enables users to generate forms using a drag-and-drop form designer. Build is implemented as an HTML5 web-based application and targets the common use case of a simple form.</li>
	<li><a href="/software/odk1/collect">Collect</a> - ODK Collect is powerful phone-based replacement for your paper forms. Collect is built on the Android platform and can collect a variety of form data types: text, location, photos, video, audio, and barcodes.</li>
	<li><a href="/software/odk1/aggregate">Aggregate</a> - ODK Aggregate provides a ready to deploy online repository to store, view and export collected data. Aggregate can run on Google's reliable and free infrastructure as well as on local servers backed by MySQL and PostgreSQL.</li>
	<li><a href="/software/odk1/form_uploader">Form Uploader</a> - ODK Form Uploader easily upload a blank form and its media files to ODK Aggregate.</li>
	<li><a href="/software/odk1/briefcase">Briefcase</a> - ODK Briefcase is the best way to transfer data from Collect and Aggregate.</li>
	<li><a href="/software/odk1/validate">Validate</a> - ODK Validate ensures that you have a OpenRosa compliant form -- one that will also work with all the ODK tools.</li>
	<li><a href="/software/odk1/xlsform">XLSForm</a> - ODK XLSForm allow XForms to be designed with Excel.</li>
</ul>

<p>The source code is available on our <a href="https://github.com/opendatakit/opendatakit">developer site</a>.</p>
