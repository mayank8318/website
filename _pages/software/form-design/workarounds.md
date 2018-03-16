---
title: Form Design Workarounds
layout: single
permalink: /software/form-design/workarounds/
date: 2018-03-01T00:00:00+00:00
sidebar:
  nav: "form-design"
toc: true
---

There are a number of awkward problems with XLSForm and the underlying XForms representation.

Nearly all of these can result in a **Force Close** of ODK Collect.

This is a loose catch-all of various work-arounds that people have reported:

## How do you remove a group or clear a field value?

If you long-press the input field (text area, radio button, etc.), a modal dialog will pop up. This dialog will always ask whether to Remove response for this field (clearing it). If the prompt is nested within a repeat group, it will also ask whether to Remove group.

## Constraints on calculate fields are not evaluated if the calculated value is empty

Assume your form prompts the user for two fields /data/name and /data/id that are not required. If you have a calculated field /data/confirmation with the following constraint:<

```xml
<bind nodeset="/data/confirmation" type="string" readonly="true()"
  calculate="concat(/data/id,if(string-length(/data/id) > 0, '', /data/name))"
  constraint="string-length(/data/id) > 0 or string-length(/data/name) > 0"
  jr:constraintMsg="You must specify either your name or your id, or both"/>
```
The constraint will never fire because the calculate evaluates to an empty string, which is then interpreted as an unset value. _And if a value is ever un-set, the constraint expression on that value will never be evaluated._ This is true even if you use the '`coalesce()`' function.

I.e., if a calculated expression evaluates to an empty string or if it evaluates to a 'NaN' value for a number, it will have the effect of clearing the prior value for the field, leaving it un-set.

The work-around is to place a `required="true()"` condition on the calculated field; or, you can change the calculation to ensure it always returns a non-empty value.

## Fields dependent upon an earlier field are not being updated

Problem: _"After answering a question in ODK collect, I expect to see an additional question displayed on the same prompt, but the screen is not being updated. The updated screen will only be displayed after going to the next prompt and then back, or after locking and unlocking the screen on the tablet. "_

This is the normal and intended behavior. If you have questions that should appear or not based upon answers to earlier questions, they cannot appear on the same screen ("field-list" group), they must appear on a subsequent screen.

ODK Collect does not recompute the relevance (visibility) of all the questions on a screen as data is entered into those questions. As a result, if you have Q2 relevance (visibility) depending upon an answer to Q1, and both are on the same screen, Q2 will be visible or hidden based upon the initial state of Q1 when the combined screen is shown, and it will never display until you leave and re-enter the screen, at which point the value of Q1 will be re-examined and Q2 will be made visible based upon Q1's (now potentially different) value.

## Field names starting with digits fail validation

Field names should not start with digits. I.e., the field name `2014crops` is not allowed, but `crops2014` is. This is requirement from the XML specification:

_The element tags are case-sensitive; the beginning and end tags must match exactly. Tag names cannot contain any of the characters !"#$%&'()*+,/;<=>?@[\]^`{|}~, nor a space character, and cannot start with -, ., or a numeric digit._

Some of our tools may vary in how strict they are in applying this rule.

## Select and select-one values disappear when editing a save form

When you re-load a form, the saved form's contents are reconstructed. During that reconstruction, each select and select-multiple prompt verifies that the saved value is among the allowed values for that prompt. If it isn't allowed, it is discarded.

This problem typically occurs because the _selection value_ (the 'name' in the XLS choices sheet), contains a space. Selection prompts split the values at spaces and match the resulting non-space-containing strings against the allowed list of values. So if your allowed list of values are `['Los Angeles','Chicago']` and you had picked and saved 'Los Angeles', when the form is re-loaded for editing, the string '`Los Angeles`' is split into `['Los', 'Angeles']`, and neither of those are in the set of allowed values, causing both values to be discarded, and your selection to be lost.

The solution is to ensure that the selection values never contain a space (e.g., change the selection value from '`Los Angeles`' to '`Los_Angeles`' and everything will work).

## Cannot store integers with 10 digits (or greater)

Integers are stored in 32-bit fields. Those which can represent integer values between (2^31)-1 and -(2^31). i.e., values between 2,147,483,647 and -2,147,483,648.

Use a string field with appearance="numbers" to enter and store larger integers.

## Decimal values are rounded

Decimal values are stored such that only the leading 15 decimal digits are preserved (they are stored in IEEE 754 double-precision (64-bit) floating point fields).

Depending upon your device, you may be able to use a string field with `appearance="numbers"` to enter and store larger decimal values (it depends upon whether your numeric keyboard layout includes a decimal point).

## Indexed-repeat failure before adding 2nd repeat group

Using XLSForm, I have a repeat and use indexed-repeat to call variables from there into the non-repeat section of the form. It works fine when the index is a static number. When the index is based on another (currently undefined, but defined before the indexed-repeat is reached) variable it crashes when transitioning from the first repetition to the second. Note that this crash is before the prompt using the indexed-repeat function has actually been reached.

My solution was to put an if on the index so it always has a value. That fixed it but I wanted to put a heads up here. I hope that is clear, if not let me know. The bottom line is, when calling from a repeat into the non-repeating part of the form:

- This doesn't work - `indexed-repeat(${name}, ${repeat}, ${id})`
- This does - `indexed-repeat(${name}, ${repeat}, if(${id} != null, ${id}, 1))`

_Clarification:_ This odd behavior occurs because whenever you alter a value, all formulas using the value are re-evaluated. Since the `${repeat}` changed (you saved and/or created a new repeat group), the formula containing the indexed-repeat is re-evaluated, but `${id}` is not yet initialized.

## Changing language Force Closes ODK Collect

The problem is that in one language you have defined only an image, and in the other language you have defined only text (for a given prompt). You need to define everything in both languages else you get the error you're seeing.

## Repeat-groups are not respecting the jr:count setting after a change

Assume you have a `jr:count="/data/count"` attribute on a repeat group named `/data/repeater`, limiting the repeat group to exactly `/data/count` records. If you then jump back to that field and enter a different value, the extraneous records are not removed.

What you can do is nest a simple group immediately within the repeat group, e.g., `/data/repeater/guard` and place a relevant condition on that group: `position(..) <= /data/count`.

This will suppress the additional records, but not delete them until you save your changes. I.e., for the lifetime of the form, `count(/data/repeater)` will equal the largest value of `/data/count` you ever entered; however, `count(/data/repeater/guard)` will equal the current value of `/data/count`. While you are editing the form, the original entries for the extra repeats are still available, but when you save the form, it will write blank values for those suppressed records. When you submit the form, there will be extra repeat records that are blank.

## Record audio does not work and/or is Force Closing ODK Collect

Beginning with Android 4.0, the shipped player appears to not respond to the standard `RECORD_SOUND_ACTION` that is defined as the action for capturing recordings.

After considerable trial-and-error testing, I found that _RecForge_ and _RecForge Lite_ apps both properly handle this action. The _RecForge_ app has the minimal permissions I'd expect for an audio recording app.

## CSV output is incorrect in Microsoft Excel

Microsoft Excel does not interpret the contents of a CSV file correctly if you simply double-click it to open the file in Excel. Instead, you must:

1. Open Excel (e.g., via the Start menu)
2. Choose Data / Get External Data From Text<
3. Choose your csv file, click Import<
4. Select Delimited
5. Select 65001: Unicode (UTF-8) for "File Origin"
6. choose Next
7. Choose Comma for the Delimiter
8. Click Next
9. Click Finish
10. Click OK to import the data starting at the highlighted cell (typically A1)

On Mac OS X, there are reports that this process does not work correctly for Arabic characters. In that case, try using any other spreadsheet program, e.g., one of the free OpenOffice.org follow-on applications, or, on Mac, the Numbers program. If you can import the data using one of those programs, you can then save it in XLSX format and then open that in Microsoft Excel.

## Dependency cycles amongst the xpath expressions in relevant/calculate

This error is caused by two or more relevant constraints or calculated fields depending upon each other's values. An example for a calculated field might be:

```xml
<bind nodeset="/data/a" calculate="/data/b + 1" type="int"/>
<bind nodeset="/data/b" calculate="/data/a + 1" type="int"/>
```

Here, the value for a depends upon b, and the value of b depends upon a. ODK Collect cannot determine how to evaluate this expression, and generates this error.

An example for a relevant condition might be:

```xml
<bind nodeset="/data/a" relevant="/data/a = 1" required="true()" type="int"/>
```

In this case, the question is relevant based upon the value the user gave for the answer to the question. Relevant conditions determine whether questions are asked, and whether their values are stored. ODK Collect cannot determine whether to ask the question because that would depend upon the user's answer!

## External itemsets do not filter properly when using integer field values

Excerpt from [opendatakit@ contribution by Hung Pham](https://groups.google.com/forum/#!topic/opendatakit/dVSIfMnnSaU):

_Using ODK's south sudan example, I was encountering an issue with filtering for external select function in xlsform._

_After some testing and examining xml & csv files, I realised that ODK Collect's `select_one_external` won't work if you have your filter as numeric values (e.g. 1, 2, 3, 4, etc) . I figured this out after changing column `name`'s value in South Sudan example (from ODK Help) to numeric value instead of short alphabetic values, then test it on ODK Collect and as expected, no choice items were displayed after "`state`". So I went back to check `itemsets.csv` files and found that all numeric values are converted in to decimal format (e.g. 1 = "1.0", 2 = "2.0", etc.) . (find attached files)_

_So that means, unless numeric values for name include ".0", ODK Collect won't be able to display cascaded selection of choices. A quick work around that I used was to remove ".0" in `itemsets.csv` file. This has work like charms._

To conclude: 2 ways of fixing numeric value sets for `select_one_external`

- Make value set in column "name" - decimal.
- Or remove ".0" in itemsets.csv file after compiling from xlsform.
