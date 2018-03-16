---
title: Form Design Cascading Selects
layout: single
permalink: /software/form-design/cascading-selects/
date: 2018-03-01T00:00:00+00:00
sidebar:
  nav: "form-design"
toc: true
---

**This page is a reference guide for users who edit the raw XML in ODK forms. If you use the XLSForm form designer, see http://xlsform.org for form design help.**

Cascading selects commonly occur in surveys. One example is choosing a state, then a county within that state, and finally a city within that county. The list of choices for the county should be narrowed to those appropriate for the chosen state, and the list of choices for the cities should be restricted to those appropriate for the chosen state and county.

Cascading selects are most easily implemented using secondary instance definitions to hold the choices. This feature is only available in version 1.2 and later of ODK Collect and ODK Aggregate.

The tuples of data values (state, county, city) that support these cascading selects are then referenced in the selection widgets through an itemset construct.

Below is a form that does this for the (state, county, city) example:

```xml
<?xml version="1.0"?>
<h:html xmlns="http://www.w3.org/2002/xforms"
  xmlns:h="http://www.w3.org/1999/xhtml"
  xmlns:ev="http://www.w3.org/2001/xml-events"
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"
  xmlns:jr="http://openrosa.org/javarosa">
<h:head>
  <h:title>Cascading Triple Select Form</h:title>
  <model>
    <itext>
      <translation lang="english">
        <text id="washington">
          <value>Washington State</value>
        </text>
        <text id="illinois">
          <value>Illinois State</value>
        </text>
        <text id="king">
          <value>King County</value>
        </text>
        <text id="pierce">
          <value>Pierce County</value>
        </text>
        <text id="douglas">
          <value>Douglas County</value>
        </text>
        <text id="cook">
          <value>Cook County</value>
        </text>
      </translation>
      <translation lang="italian">
        <text id="washington">
          <value>State of Washington</value>
        </text>
        <text id="illinois">
          <value>State of Illinois</value>
        </text>
        <text id="king">
          <value>County King</value>
        </text>
        <text id="pierce">
          <value>County Pierce</value>
        </text>
        <text id="douglas">
          <value>County Douglas</value>
        </text>
        <text id="cook">
          <value>County Cook</value>
        </text>
      </translation>
    </itext>
    <instance> <form id="CascadingTripleSelect" version="2012072301">
      <state/>
      <county/>
      <city/>
    </form>
    </instance>
      <instance id="choices">
        <states>
          <state>
            <value>washington</value>
            <counties>
              <county>
                <value>king</value>
                <cities>
                <city>
                  <name>Seattle</name>
                  <value>sea</value>
                </city>
                <city>
                  <name>Redmond</name>
                  <value>red</value>
                </city>
              </cities>
            </county>
            <county>
              <value>pierce</value>
              <cities>
                <city>
                  <name>Tacoma</name>
                  <value>tac</value>
                </city>
                <city>
                  <name>Puyallup</name>
                  <value>puy</value>
                </city>
              </cities>
            </county>
            <county>
              <value>douglas</value>
              <cities>
                <city>
                  <name>Bridgeport</name>
                  <value>bri</value>
                </city>
                <city>
                  <name>Coulee Dam</name>
                  <value>cod</value>
                </city>
                <city>
                  <name>East Wenatchee</name>
                  <value>ewe</value>
                </city>
                <city>
                  <name>Rock Island</name>
                  <value>roi</value>
                </city>
              </cities>
            </county>
          </counties>
        </state>
        <state>
          <value>illinois</value>
          <counties>
            <county>
              <value>cook</value>
              <cities>
                <city>
                  <name>Chicago</name>
                  <value>chi</value>
                </city>
                <city>
                  <name>Oak Lawn</name>
                  <value>oal</value>
                </city>
                <city>
                  <name>Oak Forest</name>
                  <value>oaf</value>
                </city>
              </cities>
            </county>
            <county>
              <value>douglas</value>
              <cities>
                <city>
                  <name>Arcola</name>
                  <value>arc</value>
                </city>
                <city>
                  <name>Tuscola</name>
                  <value>tus</value>
                </city>
                <city>
                  <name>Villa Grove</name>
                  <value>vig</value>
                </city>
              </cities>
            </county>
          </counties>
        </state>
      </states>
    </instance>
    <bind nodeset="/form/state" type="select1" />
    <bind nodeset="/form/county" type="select1" />
    <bind nodeset="/form/city" type="select1" />
  </model>
</h:head>
<h:body>
  <select1 ref="/form/state">
    <itemset nodeset="instance('choices')/states/state">
      <label ref="jr:itext(value)"/>
      <value ref="value"/>
    </itemset>
  </select1>
  <select1 ref="/form/county">
    <itemset nodeset="instance('choices')/states/state[value=/form/state]/counties/county">
      <label ref="jr:itext(value)"/>
      <value ref="value"/>
    </itemset>
  </select1>
  <select1 ref="/form/city">
    <itemset nodeset="instance('choices')/states/state[value=/form/state]/counties/county[value=/form/county]/cities/city">
      <label ref="name"/>
      <value ref="value"/>
    </itemset>
  </select1>
</h:body>
</h:html>
```
Note that there are two `<instance>` elements defined in this form. The first named instance ('`CascadingTripleSelect`') defines the data that will be sent to ODK Aggregate. This contains three string fields: '`state`', '`county`' and '`city`'.

The second named instance ('`choices`') contains the data values that will be presented to the user for their selection. This is organized as a hierarchical list of states, their counties and the cities in each county. Note that Washington and Illinois each have a Douglas county, but the cities within these two Douglas counties are entirely different.

A form can contain any number of instance elements. Only the first one is mutable. The second and subsequent instance elements are immutable. Because they are outside the first instance (and therefore do not affect the storage model on ODK Aggregate), you can alter the values in these instances (e.g., add other cities, counties and states), update the version number of the first instance, and upload this modified form to an ODK Aggregate server **WITHOUT DELETING YOUR EXISTING FORM**.

This enables you to add new menu choices while retaining all the form data that has already been submitted to ODK Aggregate for this form. The version number is defined via the version attribute of the first instance ("`2012072301`" in the above example). When uploading a modified form, the version attribute must be lexically greater than the current value. Version strings are also required to be integer values.

The key to cascading selects is the form of the `nodeset` attribute of the `<itemset>` construction. This is an XPath expression prefixed with an instance selector function; in this example, this is the `instance('choices')` piece. If that is omitted, the XPath is assumed to refer to the main instance. The instance selector takes a literal string value (it cannot be a calculated expression or a reference to a field in another instance). XPath expression syntax is explained here: [Xpath Syntax](http://www.w3schools.com/xpath/xpath_syntax.asp). Note that calculated expressions are valid within the XPath expression itself.

The expression `instance('choices')/states/state[value=/form/state]/counties/county[value=/form/county]/cities/city` searches the '`choices`' instance for all `/states/state` groups that contain a value element equal to `/form/state` in the main instance. For all such state groups, it then gathers all counties/county groups nested within these state groups that contain a value element equal to `/form/county` in the main instance. And finally, it returns all cities/city groups nested within that county group. So if `/form/state was` '`washington`' and `/form/county` was '`king`', then it would return these city elements:

```xml
<city>
  <name>Seattle</name>
  <value>sea</value>
</city>
<city>
  <name>Redmond</name>
  <value>red</value>
</city>
```

The `<label ref="name"/>` and `<value ref="value"/>` tags within the `itemset` definition are interpreted relative to the city groups in this list of values, picking out the `<name>` terms to display as the question labels, and the `<value>` terms to use as the values for those selections.

For the state and county itemsets, this form uses the `jr:itext(value)` selector to provide display strings for the states and counties. This mixture of using an element of the '`choices`' data for a display value and an `jr:itext(value)` selector is purely to control the length of the example; in a real form, you would likely choose one or the other approach for the display string. Note that the term within the `jr:itext()` selector must be a string literal or a reference to a form value.
