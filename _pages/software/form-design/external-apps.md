---
title: Form Design External Apps
layout: single
permalink: /software/form-design/external-apps/
date: 2018-03-01T00:00:00+00:00
sidebar:
  nav: "form-design"
toc: true
---

<p><span style="color:red">This page is a reference guide for users who edit the raw XML in ODK forms. If you use the <a href="../xlsform" title="XLSForm">XLSForm</a> form designer, see <a href="http://xlsform.org/">http://xlsform.org</a> for form design help.</span></p>

<p>ODK Collect can launch 3rd party apps to populate string, integer or numeric fields, and, beginning with ODK Collect 1.4.3, an external app can populate a group of fields. Also beginning with ODK Collect 1.4.3, any number of additional values, beyond the current value(s) of the field(s) being updated, can be passed to the 3rd party app. These changes were contributed by SurveyCTO. The key points are:</p>

<ol>
	<li>A text/decimal/integer field with an "ex:intentString" appearance can specify extra parameters that are passed to the external app, in addition to the "value" parameter that holds the current value for that field. The names of the parameters are user defined and there are no reserved names (except, perhaps "value"). Any number of extra parameters can be specified. The parameter values can be four different things:
	<ol>
		<li>An xpath expression to an other field.</li>
		<li>A string literal defined in single quotes.</li>
		<li>A raw number (integer or decimal)</li>
		<li>Any JavaRosa function.</li>
	</ol>
	</li>
	<li>A "field-list" group can also have an "intent" attribute.
	<ol>
		<li>This intent attribute is ONLY used when the group has an "appearance" of "field-list".</li>
		<li>The format and the functionality of the "intent" value is the same as above.</li>
		<li>The external app is launched with the parameters that are defined in the intent string PLUS the values of all the sub-fields that are either TEXT, DECIMAL, or INTEGER.</li>
		<li>Any other sub-field is invisible to the external app.</li>
		<li>If the returned bundle of values contains values whose keys match the type and the name of the sub-fields, then these values overwrite the current values of those sub-fields.</li>
	</ol>
	</li>
</ol>

<p>A sample SurveyCTO form that can be used is the following (assuming that there is an external app that handles the intent "org.myapp.COLLECT").<span style="color:#0000FF"> <strong>Newlines were inserted in the 'intent' and 'appearance' attributes of the group and the last &lt;input&gt; field to make them readable.</strong></span> The first call passes extras with the existing values for 'textFieldInGroup', 'integerFieldInGroup' and 'decimalFieldInGroup' (under those names) plus additional extras under the 'uuid' and 'deviceid' names (with the specified values) to the external app (org.myapp.COLLECT). The second call passes 'started', 'constant' and 'value' (the existing value of 'textField') to the external app (org.myapp.COLLECT).</p>

<pre>
&lt;?xml version="1.0"?&gt;
&lt;h:html xmlns="http://www.w3.org/2002/xforms"
  xmlns:ev="http://www.w3.org/2001/xml-events"
  xmlns:h="http://www.w3.org/1999/xhtml"
  xmlns:jr="http://openrosa.org/javarosa"
  xmlns:orx="http://openrosa.org/xforms/"
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"&gt;
  &lt;h:head&gt;
    &lt;h:title&gt;External Intent Test&lt;/h:title&gt;
    &lt;model&gt;
      &lt;instance&gt;
        &lt;externaltest id="externaltest" version="2013032217"&gt;
          &lt;starttime/&gt;
          &lt;endtime/&gt;
          &lt;deviceid/&gt;
          &lt;subscriberid/&gt;
          &lt;simid/&gt;
          &lt;devicephonenum/&gt;
          &lt;noteField/&gt;
          &lt;consented&gt;
            &lt;textFieldInGroup/&gt;
            &lt;integerFieldInGroup/&gt;
            &lt;decimalFieldInGroup/&gt;
          &lt;/consented&gt;
          &lt;textField/&gt;
          &lt;integerField/&gt;
          &lt;decimalField/&gt;
          &lt;meta&gt;
            &lt;instanceID/&gt;
          &lt;/meta&gt;
        &lt;/externaltest&gt;
      &lt;/instance&gt;
      &lt;bind jr:preload="timestamp"
            jr:preloadParams="start" nodeset="/externaltest/starttime" type="dateTime"/&gt;
      &lt;bind jr:preload="timestamp"
            jr:preloadParams="end" nodeset="/externaltest/endtime" type="dateTime"/&gt;
      &lt;bind jr:preload="property"
            jr:preloadParams="deviceid" nodeset="/externaltest/deviceid" type="string"/&gt;
      &lt;bind jr:preload="property"
            jr:preloadParams="subscriberid" nodeset="/externaltest/subscriberid" type="string"/&gt;
      &lt;bind jr:preload="property"
            jr:preloadParams="simserial" nodeset="/externaltest/simid" type="string"/&gt;
      &lt;bind jr:preload="property"
            jr:preloadParams="phonenumber" nodeset="/externaltest/devicephonenum" type="string"/&gt;
      &lt;bind nodeset="/externaltest/noteField"
            type="string" readonly="true()"/&gt;
      &lt;bind nodeset="/externaltest/consented"/&gt;
      &lt;bind nodeset="/externaltest/consented/textFieldInGroup"
            required="true()" type="string"/&gt;
      &lt;bind nodeset="/externaltest/consented/integerFieldInGroup"
            required="true()" type="integer"/&gt;
      &lt;bind nodeset="/externaltest/consented/decimalFieldInGroup"
            required="true()" type="decimal"/&gt;
      &lt;bind nodeset="/externaltest/textField" type="string"/&gt;
      &lt;bind calculate="concat('uuid:', uuid())"
            nodeset="/externaltest/meta/instanceID" readonly="true()" type="string"/&gt;
    &lt;/model&gt;
  &lt;/h:head&gt;
  &lt;h:body&gt;
    &lt;input ref="/externaltest/noteField" &gt;
       &lt;label&gt;Welcome again!&lt;/label&gt;
    &lt;/input&gt;
    &lt;group ref="/externaltest/consented" appearance="field-list"
            intent="org.myapp.COLLECT(uuid=/externaltest/meta/instanceID,
                                      deviceid=/externaltest/deviceid)"&gt;
      &lt;label&gt;Please populate these:&lt;/label&gt;
      &lt;input ref="/externaltest/consented/textFieldInGroup"&gt;
        &lt;label&gt;A text&lt;/label&gt;
      &lt;/input&gt;
      &lt;input ref="/externaltest/consented/integerFieldInGroup"&gt;
        &lt;label&gt;An integer&lt;/label&gt;
      &lt;/input&gt;
      &lt;input ref="/externaltest/consented/decimalFieldInGroup"&gt;
        &lt;label&gt;A decimal&lt;/label&gt;
      &lt;/input&gt;
    &lt;/group&gt;
    &lt;input appearance="ex:org.myapp.COLLECT(started= /externaltest/starttime ,
                                            constant='----', randomNumber=random())"
             ref="/externaltest/textField" &gt;
       &lt;label&gt;Click launch to see an external-fetched string&lt;/label&gt;
    &lt;/input&gt;
  &lt;/h:body&gt;
&lt;/h:html&gt;
</pre>

<p>The source code for example of an external application that collects and returns a single field value is provided, as-is, here: <a href="https://github.com/opendatakit/breathcounter">BreathCounter</a>. That project includes the form definition (.xml) file that works with the application. You will need Java and Android development experience to build the example.</p>
