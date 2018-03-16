---
title: Form Design Body
layout: single
permalink: /software/form-design/body/
date: 2018-03-01T01:00:00+00:00
sidebar:
  nav: "form-design"
toc: true
---

**This page is a reference guide for users who edit the raw XML in ODK forms. If you use the XLSForm form designer, see http://xlsform.org for form design help.**

The form body is what is actually displayed to the user. Each body element must reference one of the nodes in the instance using the operator `ref=""`.

## String, Integer, Decimal, Date, Geopoint, Barcode

```xml
<input ref="node1">
  <label>prompt label</label>
  <hint>optional prompt hint</hint>
</input>
```

## Select multi

```xml
<!-- the <label> for each element is what the user will see. -->
<!-- the <value> will be what gets sent with the data. -->
<!-- Note: text between the <value> tags must not contain spaces. -->
<select ref="node2">
  <label>Please select colors you like</label>
  <hint>You can pick several, or none</hint>
  <item>
    <label>Blue</label>
    <value>blue</value>
  </item>
  <item>
    <label>Green</label>
    <value>green</value>
  </item>
  <item>
    <label>Yellow</label>
    <value>yell</value>
  </item>
  <item>
    <label>Red</label>
    <value>red</value>
  </item>
</select>
```

## Select one

```xml
<!-- the <label> for each element is what the user will see. -->
<!-- the <value> will be what gets sent with the data. -->
<!-- note: text between the <value> tags must not contain spaces. -->
<select1 ref="node3">
  <label>Please select your favorite color</label>
  <hint>you can only pick one</hint>
  <item>
    <label>Blue</label>
    <value>blue</value>
  </item>
  <item>
    <label>Green</label>
    <value>green</value>
  </item>
  <item>
    <label>Yellow</label>
    <value>yell</value>
  </item>
  <item>
    <label>Red</label>
    <value>red</value>
  </item>
</select1>
```

## Capture image, audio, or video

```xml
<!-- image -->
<upload ref="node5" mediatype="image/*">
  <hint>this will launch the camera or image chooser</hint>
  <label>image prompt</label>
</upload>

<!-- audio -->
<upload ref="node6" mediatype="audio/*">
  <hint>this will launch the audio recorder or sound chooser</hint>
  <label>audio prompt</label>
</upload>

<!-- video -->
<upload ref="node7" mediatype="video/*">
  <label>this will launch the camcorder or video chooser</label>
</upload>
```

## Multiple prompts in a single screen, logical, labeled, or repeated groups of prompts

ODK Collect does not recompute the relevance (visibility) of all the questions on a screen as data is entered into those questions. As a result, if you have Q2 relevance (visibility) depending upon an answer to Q1, and both are on the same screen, Q2 will be visible or hidden based upon the initial state of Q1 when the combined screen is shown, and it will never display until you leave and re-enter the screen, at which point the value of Q1 will be re-examined and Q2 will be made visible based upon Q1's (now potentially different) value.

```xml
<!-- plain group -->
<group>
  <label>household</label>
  <input ref="name">
    <label>name</label>
  </input>
  <input ref="age">
    <label>age</label>
  </input>
</group>

<!-- repeated group -->
<!-- note: /data/household must be defined as instance variables -->
<group>
  <label>household</label>
  <repeat nodeset="/data/household">
    <input ref="name">
      <label>name</label>
    </input>
    <input ref="age">
      <label>age</label>
    </input>
  </repeat>
</group>

<!-- multiple prompts per screen -->
<group appearance="field-list">
  <label>household</label>
  <input ref="name">
    <label>name</label>
  </input>
  <input ref="age">
    <label>age</label>
  </input>
</group>
```

## Use a previous answer in your prompt text

```xml
<input ref="node9">
  <label>Are you sure <output value="/data/name"/> is your name?</label>
</input>
```
## Branching on a group

```xml
<!-- instance -->
<group_b>
  <question_b1/>
  <question_b2/>
</group_b>

<!-- bind -->
<bind nodeset="/data/group_b" type="string"
 relevant="selected(/data/branch, 'b')"/>

<!-- body -->
<!-- /data/branch instance must be defined and bound as a select1 -->
<group ref="/data/group_b">
  <input ref="/data/group_b/question_b1">
    <label>question b1</label>
  </input>
  <input ref="/data/group_b/question_b2">
    <label>question b2</label>
  </input>
</group>
```

## Repeating prompts a fixed number of times

``` xml
<!-- /data/repeat_* nodes must be defined as an instance variable -->
<group>
  <label>repeat node a</label>
  <repeat nodeset="/data/repeat_node_a" jr:count="/data/repeat_count_a">
    <input ref="/data/repeat_node_a/repeat_string_a">
      <label>this should repeat <output value="/data/repeat_count_a"/>
        times and finish</label>
    </input>
  </repeat>
</group>
```

## Ask enumerator to acknowledge a prompt

```xml
<trigger ref="node4">
  <label>trigger prompt</label>
  <hint>need to push button</hint>
</trigger>
```
