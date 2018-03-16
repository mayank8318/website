---
title: Frequently Asked Questions
date: 2018-03-01T00:00:00+00:00
layout: single
permalink: /about/faq/
author_profile: false
sidebar:
  nav: "about"
toc: true
toc_label: "Questions"
toc_icon: "question-circle"

excerpt: "Truth be told, these questions aren't frequently asked. Hopefully the answers are still helpful."
header:
  overlay_image: /assets/odk/banner.jpg
  overlay_filter: rgba(255, 0, 0, 0.5)
  caption: "Photo credit: [**TBD**](https://example.com)"

---

## What is ODK?

<p>Open Data Kit (ODK) is a free and open-source set of tools which help organizations create mobile data collection solutions. Our <a href="/blog">blog</a> and <a href="/about/deployments/">deployments page</a> have good examples of what others have used ODK for. Our <a href="/about/research/">research page</a> also has videos and papers that explain ODK.</p>

## How do I use ODK?

<p>Please read through the documentation on our <a href="/1_0_tools/usage_documentation">implementer instructions</a> and on the <a href="https://github.com/opendatakit/opendatakit/wiki">developer wiki</a>. If that doesn't help, search the <a href="https://forum.opendatakit.org/">community forum</a>, or one of the no longer used <a href="https://groups.google.com/group/opendatakit">opendatakit@googlegroups.com</a> general mailing list, and <a href="https://groups.google.com/group/opendatakit-developers">opendatakit-developers@googlegroups.com</a> (for coding questions) to see if the issue has been answered. If you don't find an answer after searching, then feel free to ask on the.<a href="https://forum.opendatakit.org/">community forum</a> or the <a href="https://opendatakit.slack.com">OpenDataKit Slack</a></p>

## What kinds of questions do you answer on the forum?

<p>Our team only answers questions about the <a href="/toolselector">supported tools</a>. We generally do not answer form design questions, and instead refer you to the <a href="/1_0_tools/usage_documentation/form_design">form design</a> guide. You are more than welcome to post any message -- someone else in the community is likely to help.</p>

## An ODK tool isn't working the way I expected. What do I do?

<p>Make sure you are running the latest versions of ODK software. You can find them under our <a href="/1_0_tools/download">downloads</a> page. Search the <a href="https://github.com/opendatakit/opendatakit/issues">issue tracker</a> to see if the problem you are having has been reported. If you can't find it, report it there. Please be precise about the tool you are using, the version of the software, and include all the steps you did so we can reproduce the same problem. If you can get a stack trace, please attach it. If the problem is with a form, please attach it as well. If you are new to filing bug reports, read <a href="http://www.chiark.greenend.org.uk/~sgtatham/bugs.html">How to Report Bugs Effectively</a>. If your issue is urgent, we recommend you <a href="/support/help_for_hire">hire help</a> from one of the ODK implementations companies.</p>

## How do I get a stack trace or log after an Android "Force Close"?

<p>See <a href="https://github.com/opendatakit/opendatakit/wiki/Collect-Troubleshooting">Collect Troubleshooting</a>. Capturing an error log is more difficult now that the newer Android operating systems restrict access to the system log stream. Once you begin capturing a log and have reproduced the crash, please open an issue <a href="https://github.com/opendatakit/opendatakit/issues">here</a> and attach the captured log file.</p>

## How do I request a new feature or enhancement?

<p>Search the <a href="https://github.com/opendatakit/opendatakit/issues">issue tracker</a> to see if the feature you want has been suggested. If you find it, vote for it by adding yourself to receive notifications. If you don't find it, open a new issue (feature request) describing the scenario which you need the feature for.</p>

## How do I customize or implement an ODK solution?

<p>The core team does not provide code or implementation support beyond what is described on our <a href="/">implementer site</a> and on the <a href="https://github.com/opendatakit/opendatakit">developer site</a>. If you need more support, <a href="/support/help-for-hire/">hire help</a> from one of the ODK implementations companies.</p>

## How should I cite ODK in a publication?

<p>People often ask "How do I cite ODK?". Since Open Data Kit is an academic research project, please cite the academic research papers corresponding to the appropriate tool version.</p>

<p>If you are using ODK tools with a version code 1.x cite:</p>

<p><a href="/sites/opendatakit-dev.cs.washington.edu/files/images/ODK-Paper-ICTD-2010.pdf">Open Data Kit: Tools to Build Information Services for Developing Regions </a>Carl Hartung, Yaw Anokwa, Waylon Brunette, Adam Lerer, Clint Tseng, Gaetano Borriello In ICTD, 2010. <a href="http://dl.acm.org/citation.cfm?id=2369236">http://dl.acm.org/citation.cfm?id=2369236</a></p>

<p>If you are using ODK tools with a version code 2.x cite:</p>

<p><a href="http://www.hotmobile.org/2013/papers/full/2.pdf">Open Data Kit 2.0: Expanding and Refining Information Services for Developing Regions</a> Waylon Brunette, Mitchell Sundt, Nicola Dell, Rohit Chaudhri, Nathan Breit, Gaetano Borriello In HotMobile, 2013. <a href="http://dl.acm.org/citation.cfm?id=2444790">http://dl.acm.org/citation.cfm?id=2444790</a></p>

<p>Other publications to cite for individual ODK tools are available on the <a href="/about/research/">Research </a>page.</p>

## Are there other data collection systems I should consider?

<p>Of course! There are many other data collection systems that might work better for you. Some of them use ODK in some way (<a href="http://ona.io">Ona</a>, <a href="http://www.surveycto.com">Survey CTO</a>, <a href="http://kobotoolbox.org">KoBo Toolbox</a>, <a href="http://commcarehq.com">Commcare HQ</a>, <a href="http://doforms.com">DoForms</a>, <a href="http://datawinners.com">DataWinners</a>, <a href="http://viewworld.dk">ViewWorld</a>, <a href="http://webfirst.com/phicollect">PhiCollect</a>) while others are ODK compatible (<a href="http://www.dimagi.com/javarosa/">JavaRosa</a>, <a href="http://www.openxdata.org/">OpenXData</a>, <a href="http://rapidsms.org">RapidSMS</a>). There are also great systems that were designed more for SMS (<a href="http://www.frontlinesms.com">FrontlineSMS</a>, <a href="http://www.ushahidi.com">Ushahidi</a>), systems that work on iOS (<a href="http://www.iformbuilder.com/">iFormBuilder</a>), even systems that work on Palm Pilots and Windows Mobile (<a href="http://pendragonsoftware.com/forms3/index.html">Pendragon Forms</a>, <a href="http://cybertracker.org/">CyberTracker</a>) and Nokias (<a href="http://www.nokia.com/corporate-responsibility/society/nokia-data-gathering/english">Nokia Data Gathering</a>). If you want to find out more, <a href="http://mobileactive.org">MobileActive</a> is a great place to learn more about data collection. <a href="https://docs.google.com/spreadsheet/ccc?key=0Akj5_3vVWZ8tdGk4czI4eHcycGo2Y1NnWmhsUjdBTXc&amp;hl=en_US">Mobile Data Collection Tools - Comparison Matrix</a> and <a href="https://docs.google.com/spreadsheet/ccc?key=0ArG7kkc9mE75dEdNNktocmVwT0hNbHVjTXl2ZU1VMXc&amp;hl=en_US">Mobile-Phone-Based Data Collection Systems Comparison Table</a>, <a href="http://public.webfoundation.org/2011/01/MW4D_WS/report">Mobile and Web Technologies for Social and Economic Development</a> report, <a href="https://sites.google.com/site/dougbrowningportfolio/Resources/mobile-gis">Comparing Mobile Solutions for GIS Data Collection and Display</a>, and <a href="http://humanitarian-nomad.org/?page_id=533">Nomad Mobile Collection Systems Decision Tool</a> are also good resources. We also have <a href="//opendatakit.org/about/research/">peer-reviewed research</a> and <a href="//opendatakit.org/blog">user stories</a> that describe the situations where ODK is likely to be easier to use, less error-prone, more cost-effective and more timely when compared to other data collection systems.</p>

## Should I email members of the ODK team directly?

<p>Probably not. If you have a private question you cannot post to the list, please send it to <a href="mailto:contact@opendatakit.org">contact@opendatakit.org</a>.</p>

## What Android phone/tablet/device should I use?

<p>The Android ecosystem changes too rapidly to recommend one device. In general, we recommend you get devices that you can source in-country and run the latest Android OS (even though we support Android OS 1.6+ and higher). ODK Collect will run on most Android form factors (including tablets and netbooks). We recommend you spend a little more to get a higher quality device, instead of buying the cheapest phone. If you need a supplier, try <a href="http://amazon.com">amazon.com</a>, <a href="http://newegg.com">newegg.com</a>, <a href="http://ebay.com">ebay.com</a>, <a href="http://www.n1wireless.com">n1wireless.com</a>, <a href="http://www.expansys-usa.com/android-smartphones/">expansys-usa.com</a>&nbsp;and <a href="http://negrielectronics.com">negrielectronics.com</a>. For a list of all Android devices, try <a href="http://en.wikipedia.org/wiki/List_of_Android_devices">wikipedia.org</a>, <a href="http://gsmarena.com">gsmarena.com</a>, and <a href="http://phonescoop.com">phonescoop.com</a>.</p>
