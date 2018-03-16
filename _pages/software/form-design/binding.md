---
title: Form Design Binding
layout: single
permalink: /software/form-design/binding/
date: 2018-03-01T00:00:00+00:00
sidebar:
  nav: "form-design"
toc: true
---

**This page is a reference guide for users who edit the raw XML in ODK forms. If you use the [XLSForm](/software/odk1/xlsform/) form designer, see http://xlsform.org/ for form design help.**

Bindings are where you specify data types, constraints, branching, and any other form logic. An example is shown below.

``` xml
<bind nodeset="/data/branch" type="select1"/>
<bind nodeset="/data/mystring" type="string"
  relevant="selected(/widgets/branch, 'n')"/>
```

Below is a table of the supported keywords and operators. Our documentation may fall out of date, so if you are a developer, you can get a more updated list in the JavaRosa [source code](https://bitbucket.org/m.sundt/javarosa/src/4622e5cd9d62b759097a80c5130adfdb667c01f0/core/src/org/javarosa/xpath/expr/XPathFuncExpr.java?at=default&amp;fileviewer=file-view-default#XPathFuncExpr.java-142).

## Keyword

<table>
	<tbody>
		<tr>
			<th>Keyword</th>
			<th>Usage</th>
		</tr>
		<tr>
			<td>nodeset</td>
			<td>Specify which instance element this binding is referring to</td>
		</tr>
		<tr>
			<td>relevant</td>
			<td>Relevancy is how to branch through a form. If a node is not relevant, it doesn't appear to the user</td>
		</tr>
		<tr>
			<td>readonly</td>
			<td>If a node is read only, the user will only be able to view that prompt, not enter data</td>
		</tr>
		<tr>
			<td>required</td>
			<td>A required field will not allow a blank or empty answer before proceeding</td>
		</tr>
		<tr>
			<td>constraint</td>
			<td>Constraint allows you to specify acceptable answers for the specified prompt</td>
		</tr>
		<tr>
			<td>type</td>
			<td>Data type</td>
		</tr>
		<tr>
			<td>calculate</td>
			<td>Allows you to run a calculation using this and/or other answers</td>
		</tr>
		<tr>
			<td>jr:constraintMsg</td>
			<td>The message that will be displayed if the specified constraint is violated</td>
		</tr>
		<tr>
			<td>jr:preload</td>
			<td>JavaRosa provides preloaders that can automatically give you information about the form. These are discussed below</td>
		</tr>
		<tr>
			<td>jr:preloadParams</td>
			<td>Parameters used by jr:preload</td>
		</tr>
		<tr>
			<td>jr:count</td>
			<td>References a number used to determine number of repeats. Only used in the &lt;body&gt;</td>
		</tr>
	</tbody>
</table>

## Operators

The following list details various operators: usage, an example, and notes for each.

### This current prompt's answer
- **Usage:** `.`
- **Example:** `constraint=". < 10.51"`
- **Notes:** If current answer is less than 10.51

### The current prompt's enclosing group
- **Usage:** `..`
- **Example:** `constraint=". < ../q1"`
- **Notes:** If current answer is less than the value of the 'q1' prompt within this same group.

### not
- **Usage:** `not(expression)`
- **Example:** `relevant="not(selected(/widgets/select1, 'c'))"`
- **Notes:** As long as 'c' is not selected in /widgets/select1

### and
- **Usage:** `and`
- **Example:** `constraint="selected(., 'c') and selected(., 'd')"`
- **Notes:** Both 'c' and 'd' need to be selected in the current prompt<

### or*
- **Usage:** `or`
- **Example:** `constraint="selected(., 'c') or selected(., 'd')"`
- **Notes:** Either 'c' or 'd' needs to be selected in the current prompt

### Conditional
- **Usage:** if(condition, a, b)
- **Example:** `calculate="if(selected(/data/q1, 'yes') and selected(/data/q2, 'yes'), 'yes', 'no')"`
- **Notes:** If true return a, else return b

### Equal to, or, (not equal to)
- **Usage:** `=` _-or-_ `!=`
- **Example:** `constraint=". = number('10')"`
- **Notes:** Current answer must be equal to 10

### Greater than, or, (or equal)
- **Usage:** `>=`
- **Example:** `constraint=". > 10.51"`
- **Notes:** Greater than 10.51, can also be combined with equals: `>=` **NOTE:** XLSForm and Build translate `>` into `&amp;gt;` within the XML file (`>` is a reserved character in XML).

### Less than, or, (or equal)
- **Usage:** `<=`
- **Example:** `constraint=". < 10.51"`
- **Notes:** Less than 10.51, can also be combined with equals: `<=` **NOTE:** XLSForm and Build translate `<` into `&amp;lt;` within the XML file (`<` is a reserved character in XML).

### Addition and subtraction
- **Usage:** `+` _-or-_ `-`
- **Example:** `constraint="(. + ../q1) < 10.51"</td>`
- **Notes:**  This value plus the value of 'q1' is less than 10.51.

### Multiplication and division
- **Usage:** `*` or div
- **Example:** `constraint="(. div ../q1) < 10.51"`
- **Notes:** This value divided by the value of 'q1' is less than 10.51

### Modulo (e.g., testing for even/odd values)
- **Usage:** `mod`
- **Example:** `constraint="(. mod 2) = 0"`
- **Notes:** This value is an even number (this value modulo 2 is zero)

### Selected
- **Usage:** `selected(xpath/to/node, value)`
- **Example:** `relevant="selected(/widgets/branch, 'n')"`
- **Notes:** Checks if answer in selected prompt is selected

### jr:choice-name
- **Usage:** `jr:choice-name(value, 'xpath/to/node')`
- **Example:** `calculate="if(string-length(/widgets/yesno)!=0,jr:choice-name(/widgets/yesno,'/widgets/yesno'),'unspecified')"`
- **Notes:** If `/widgets/yesno` has a value selected, obtain the display string for it. This will be in the currently selected display language. **NOTE:** the list of choices cannot use filter conditions (it cannot be a cascading-select list). The bracketing if(...) is needed due to a limitation in javarosa ([issue 921](https://github.com/opendatakit/opendatakit/issues/921)).

### (n+1)th selected value
- **Usage:** `selected-at(xpath/to/node, position)`
- **Example:** `selected-at(multi-select, 3)`
- **Notes:** Return the (position+1)th (e.g., 4th) selected value in a multiple-choice select.

### Count selected
- **Usage:** `count-selected(xpath/to/value)`
- **Example:** `count-selected(multi-select)`
- **Notes:** Return the number of selected answers

### Field within n-th repeat group
- **Usage:** `indexed-repeat(field,group,index, subgroup,subidx, ssgrp,ssidx,...)`
- **Example:** `indexed-repeat(/widgets/names/name,/widgets/names,1)`
- **Notes:** References the field of the n-th repeat of a group. Groups and indices for 1 to 3 nested repeats can be specified. For example, the XLSForm calculate expression "indexed-repeat(${name}, ${names}, 1)" will return the value of the first "name" field inside a repeat group named "names".

### True
- **Usage:** `true()`
- **Example:** `required="true()"`

### False
- **Usage:** `false()`
- **Example:** `required="false()"`

### Convert to boolean<
- **Usage:** `boolean (xpath/to/node or value)`
- **Example:** `relevant="boolean(/widgets/branch)"`
- **Notes:** Conversion varies depending on data type of x

### Boolean from string
- **Usage:** `boolean-from-string(xpath/to/node)`
- **Example:** `boolean-from-string (xpath/to/node)`
- **Notes:** Returns true if x is "true" or "1", false otherwise. note that this is different behaviour from boolean(x)

### Convert to number
- **Usage:** `number (xpath/to/node or value)`
- **Example:** `constraint=". < number(/data/age)"`
- **Notes:** Conversion varies depending on data type of x

### date, dateTime, time as number
- **Usage:** `decimal-date-time (xpath/to/node or value)` _-or-_ `decimal-time (xpath/to/node or value)`
- **Example:** `constraint="decimal-date-time(.) - decimal-date-time(../q1) < 5"`
- **Notes:** This date is within 5 days of 'q1' date. The unit of conversion is one day. Date and date-time values can be truncated or rounded by other logic within Javarosa; please verify these functions work as you intend before relying upon them!

### Convert to integer
- **Usage:** `int (xpath/to/node or value)`
- **Example:** `constraint=". < int(/data/age)"`
- **Notes:** Conversion varies depending on data type of x

### Convert to string
- **Usage:** `string (xpath/to/node or value)`
- **Example:** `"string (/data/age)"`
- **Notes:** Conversion varies depending on data type of x

### Date, date-time, formatted as string
- **Usage:** `format-date(xpath/to/node, format)` _-or-_ `format-date-time(xpath/to/node, format)``
- **Example:** `format-date (xpath/to/node, '%Y/%n/%e %H:%M')`
- **Notes:** Returns the date value at the `xpath/to/node` formatted as defined by the format argument. **NOTE:** date-time values may be truncated or rounded by other logic within Javarosa; please verify behavior before relying upon this operation. See [Format Source Code](https://bitbucket.org/m.sundt/javarosa/src/62409ae3b803/core/src/org/javarosa/core/model/utils/DateUtils.java#cl-247) for available `'%'` format specifiers.

### Convert to date
- **Usage:** `date (xpath/to/node or value)`
- **Example:** `constraint=". >= date('2011-11-12')"`
- **Notes:** Conversion varies depending on data type of x. Format is yyyy-mm-dd

### Regular expression
- **Usage:** `regex(xpath/to/node, regular expression)`
- **Example:** `constraint="regex(., '[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,4}')"`
- **Notes:** This particular regex checks for a valid email address. See <a href="">[Regex Patterns](https://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html). Complex patterns may cause ODK Collect to force close due to execution stack overflow.

### First non-empty value
- **Usage:** `coalesce(a, b)`
- **Example:** `calculate="coalesce(/data/name, /data/national_id)"`
- **Notes:** If name has a value, return name, else return national_id

### Concatenated string values
- **Usage:** `concat(xpath/to/value1, xpath/to/value2, ...)`
- **Example:** `calculate="concat(/data/name, ' with id: ', /data/national_id)"`
- **Notes:** Returns the concatenation of the string values.

### Concatenate string values with a separator string
- **Usage:** `join(separatorString, nodeset) join(separatorString, xpath/to/value1, xpath/to/value2, ...)`
- **Example:** `calculate="concat('The children of the household are: ', join(', ', /data/household/childname))"`
- **Notes:** Returns the concatenation of the string values using the first argument as a separator between values.

### Extract a substring
- **Usage:** substr(xpath/to/value, start) substr(xpath/to/value, start, end)
- **Example:** `calculate="substr('Test',1,2)='e'"`
- **Notes:** Returns the substring beginning at the specified start and extends to the character at index end - 1. start and end begin at '0'.

### Length of a string
- **Usage:** `string-length(xpath/to/value)`
- **Example:** `calculate="string-length('Test')=4"`
- **Notes:** return the length of a non-empty string

### count(nodeset)
- **Usage:** `count(nodeset)`
- **Example:** `count(nodeset)`
- **Notes:** Count the number of nodes in nodeset

### sum(nodeset)
- **Usage:** `sum(nodeset)`
- **Example:** `sum(nodeset)`
- **Notes:** Return the sum of the values of the nodes in nodeset

### max(nodeset)
- **Usage:** `max(nodeset)`
- **Example:** `max(nodeset)`
- **Notes:** Return the maximum of the values of the nodes in nodeset

### min(nodeset)
- **Usage:** `min(nodeset)`
- **Example:** `min(nodeset)`
- **Notes:** Return the minimum of the values of the nodes in node set

### round(value, power)
- **Usage:** `round(xpath/to/value, power)`
- **Example:** `calculate="round(/data/q1, 3)"`
- **Notes:** Return the rounded value of q1, as in Excel

### pow(value, power)
- **Usage:** `pow(xpath/to/value, power)`
- **Example:** `calculate="pow(/data/q1, 3)"`
- **Notes:** Return the cube of q1 (q1 raised to the 3rd power).

### today()
- **Usage:** `today()`
- **Example:** `today()`
- **Notes:** Return today's date

### now()
- **Usage:** `now()`
- **Example:** `now()`
- **Notes:** Return a timestamp for this instant

### once(expr)
- **Usage:** `once(expr)`
- **Example:** `once(random()*3)`
- **Notes:** If the field already has a value, return the existing value, otherwise evaluate the expression to provide a value.

### random()
- **Usage:** `random()`
- **Example:** `random()`
- **Notes:** Return a random number between 0.0 (inclusive) and 1.0 (exclusive). You should wrap this in once()

### uuid()
- **Usage:** `uuid()`
- **Example:** `uuid()`
- **Notes:** Return a random UUID string

### at least X of, at most X of
- **Usage:** `checklist(min, max, v1, v2, v3, ..., vn)`
- **Example:** `checklist(min, max, v1, v2, v3, ..., vn)`
- **Notes:** V1 through vn are a set of n yes/no answers. Return TRUE if the count of 'yes' is between minimum and maximum, inclusive. Minimum or maximum may each be -1 to indicate 'not applicable'.

### weighted at least X of, at most X of
- **Usage:** `weighted-checklist(min, max, v1, w1, v2, w2, v3, w3, ..., vn, wn`
- **Example:** `weighted-checklist(min, max, v1, w1, v2, w2, v3, w3, ..., vn, wn)`
- **Notes:** V1 through vn are a set of n yes/no answers. w1 through wn are weights of the 'yes' answers to those questions. Return TRUE if the weighted sum of 'yes' is between minimum and maximum, inclusive. Minimum or maximum may each be -1 to indicate 'not applicable'.

### get property value
- **Usage:** `property(name_of_property)`
- **Example:** `property('deviceid')`
- **Notes:** Return the deviceid property value

### position(xpath)
- **Usage:** `position(xpath)`
- **Example:** `position(..)`
- **Notes:** Return the XML position() value of this node in a filtered XPath expression. Note that position() does NOT work.</td>

## Additional common binding examples

Below are common examples of bindings that may be useful. Since these show the actual XML of the bind statement, the > and < symbols are written as `&amp;gt;` and `&amp;lt;` (> and < are reserved characters in XML files).

## Simple String

```XML
<bind nodeset="/widgets/mystring" type="string"/>
```

## Required Integer

```xml
<bind nodeset="/widgets/int" type="int" required="true()"/>
```
## Branching

### Show this prompt if the answer to /widget/int is less than 8

```xml
<bind nodeset="/widgets/int2" type="int" relevant="/widgets/int &amp;lt; 8"/>
```

### Show this prompt if the answer to /widget/branch (a select1) is "n"

```xml
<!-- the value 'n' is the <value>, not the <label> in  the <item> in the select or select1 -->
<bind nodeset="/widgets/language" type="string"
  relevant="selected(/widgets/branch, 'n')"/>
```

## Constraints

### Answer must be after date set in /widgets/date1

```xml
<bind nodeset="/widgets/date2" type="date"
  constraint=". > /widgets/date1"
  jr:constraintMsg="date must be after /widgets/date1"/>
```

### Answer must be after today

```xml
<bind nodeset="/widgets/date" type="date"
  constraint=". > today()"
  jr:constraintMsg="only future dates allowed"/>
```

### Answer must between 4 and 10 characters long (inclusive)

```xml
<bind nodeset="/widgets/string"
   type="string" constraint="string-length(.) &amp;gt;= 4 and string-length(.) &amp;lt;= 10"/>
```

### Answer must be lowercase letters and between 1 and 10 characters long (inclusive)

```xml
<bind nodeset="/widgets/string"
   type="string" constraint="(regex(., "^[a-z]{1,10}$"))"/>
```

### "c" and "d" cannot be selected at the same time

```xml
<bind nodeset="/widgets/select" type="select"
  constraint="not(selected(., 'c') and selected(., 'd'))"
  jr:constraintMsg="option c and d cannot be selected together"/>
```

### Multi-lingual constraint message

```xml
<!-- use itext to define various language text -->
<bind nodeset="/data/prompt" type="int" constraint=". &amp;lt;= 10"
    jr:constraintMsg="jr:itext('/data/prompt:error_message')"/>
```

## Regular Expression

### Answer must be an email address like bob@aol.com

```xml
<bind nodeset="/widgets/regex" type="string" required="true()"
 constraint="regex(., '[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,4}')"
 jr:constraintMsg="this isn't a valid email address"/>
 ```

## Repeat a group N times

(Where N is an answer to another prompt in the form.)

```xml
<!--  rare cases where the binding is defined in the body -->
<group>
  <label>repeat node a</label>
  <repeat nodeset="/data/repeat_node_a" jr:count="/data/repeat_count_a"
    jr:noAddRemove="true()">
    <input ref="/data/repeat_node_a/repeat_string_a">
      <label>this should repeat <output value="/data/repeat_count_a"/>
        times and finish</label>
    </input>
  </repeat>
</group>
```

## Setting a relevant condition on a repeat (or non-repeat) group

```xml
<!--  you can set relevant conditions on groups and repeats -->
    <model>
      <instance>
        <data id="build_TestForm_1331813278">
          <id/>
          <add_cate jr:template="">
            <name/>
          </add_cate>
        </data>
      </instance>
      <bind nodeset="/data/id" type="string" required="true()"/>
      <bind nodeset="/data/add_cate" relevant="(/data/id = '100')"/>
      <bind nodeset="/data/add_cate/name" type="string"/>
    </model>
...
    <input ref="/data/id">
      <label>ID:</label>
      <hint>Entering 100 will skip repeat group</hint>
    </input>
    <group>
      <label>Additional Categories</label>
      <repeat nodeset="/data/add_cate" appearance="field-list">
        <input ref="/data/add_cate/name">
          <label>Name:</label>
        </input>
      </repeat>
    </group>
```

You can add the binds below to your form for hidden or pre-loaded fields you want automatically filled in. You'll need a variable for them in the instance and a binding, but they have no body element and the user will never see or interact with them. A more complete list of the available `jr:preloadParams` values is available [here](/software/form-design/examples/).

## Form start time

```xml
<!--  stored the first time the form is loaded -->
<bind nodeset="/widgets/start_time" type="dateTime"
 jr:preload="timestamp"
 jr:preloadParams="start"/>
```

## Form end time

```xml
<!--  updated every time the form is saved -->
<bind nodeset="/widgets/end_time" type="dateTime"
 jr:preload="timestamp"
 jr:preloadParams="end"/>
 ```

## Current date

```xml
<bind nodeset="/widgets/date_today" type="date"
 jr:preload="date"
 jr:preloadParams="today"/>
```

## Device ID (IMEI)

```xml
<bind nodeset="/widgets/deviceid" type="string"
 jr:preload="property"
 jr:preloadParams="deviceid"/>
```

## Subscriber ID (IMSI)

```xml
<bind nodeset="/widgets/my_subscriberid" type="string"
 jr:preload="property"
 jr:preloadParams="subscriberid"/>
```

## SIM serial number

``` xml
<bind nodeset="/widgets/my_simid" type="string"
 jr:preload="property"
 jr:preloadParams="simserial"/>
 ```

## Device phone number

``` xml
<bind nodeset="/widgets/my_phonenumber" type="string"
 jr:preload="property"
 jr:preloadParams="phonenumber"/>
 ```
