---
title: Form Design External Itemsets
layout: single
permalink: /software/form-design/external-itemsets/
date: 2018-03-01T00:00:00+00:00
sidebar:
  nav: "form-design"
toc: true
---


If your form has selects with a large number of items (e.g., hundreds), that form can slow down ODK Collect's form loading and navigation. The best workaround to this issue is to use external itemsets (ODK Collect v1.4 r1033 or later).

To use external itemsets, start with a normal XLS file and use XLSForm to convert it to an XForm. Take that XForm and do the following.

1. Delete any `<itext>` references for values in your itemsets
2. Delete all extra `<instance>...</instance>` except for the first one
3. In the section, wherever you see `<itemset nodeset="...">` cut/paste the `nodeset="..."` into the `<select1>` element for that node

```xml
<select1 ref="/new_cascading_select/county"
   nodeset="instance('counties')/root/item[state=/new_cascading_select/state]">
```

{:start="4"}
4. Rename '`nodeset`' to '`query`'

```xml
<select1 ref="/new_cascading_select/county"
   query="instance('counties')/root/item[state=/new_cascading_select/state]">
```

{:start="5"}
5. Rename the `<select1 ...>` and `</select1>` nodes to '`input`'

```xml
<input ref="/new_cascading_select/county"
   query="instance('counties')/root/item[state=/new_cascading_select/state]">
```

{:start="6"}
6. Remove the `<itemset ...>` and `</itemset>` nodes

7. Remove any `<value ref="..."/>` and `<label ref=""/>` inside of the `<input>` with the `query="..."`

8. In the `<bind nodset="..."` change the `type="select1"` to `type="string"` for any of your new itemsets

9. From the .xls file, save the sheet '`choices`' as '`itemsets.csv`'

10. Put `itemsets.csv` in the `[form-filename]-media` folder on the device

11. If you don't have any explicit languages defined in the form, you also have to add the following after `<model>`:

```xml
<itext><translation default="true()" lang="default"/></itext>
```

If you need more help, download the [external itemsets example](/download/odk1/). The example includes four files that should make external itemsets easier to understand.

You will get a `cascading_select.xls` file with normal itemsets, the normal `cascading_select.xml` file created by XLSForm, an updated `cascading_select_external_itemsets.xml` file modified to work with the external itemsets, and the `itemsets.csv` that goes along with the updated `cascading_select_external_itemsets.xml` file.
