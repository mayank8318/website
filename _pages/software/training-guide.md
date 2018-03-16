---
title: An ODK Training Guide
layout: single
permalink: /software/training-guide/
date: 2018-03-01T00:00:00+00:00
sidebar:
  nav: "software"
toc: true
---

Below is a training guide written by Neil Hendrick (from [Harvard Humanitarian Initiative](http://hhi.harvard.edu/) and [Kobo](http://www.kobotoolbox.org/)) about how to train enumerators to get good data using ODK. While many of the lessons below are applicable across various deployments, others have shared their own training techniques and experiences using ODK in different scenarios and cultures.

  * Yaw Anokwa from Nafundi: [Replacing paper forms with smart forms on phones and tablets](https://speakerdeck.com/nafundi/replacing-paper-forms-with-smart-forms-on-phones-and-tablets)
  * Emily Kumpel and Berkeley in India: [Deployment Manual](http://ekumpel.wordpress.com/2011/02/13/135/)
  * Neil Hendrick and Berkeley HRC in Liberia: [Deployment Notes](https://groups.google.com/group/opendatakit/browse_thread/thread/482acd1de955692e)
  * Andrew Azman and Johns Hopkins in Ghana: [Deployment Notes](https://groups.google.com/group/opendatakit/browse_thread/thread/482acd1de955692e)
  * Evelyn Castle in Nigeria: [Training Manual](http://www.evelyncastle.com/wp-content/uploads/2012/01/Users_Manual.pdf), Videos on [using Android](https://www.youtube.com/watch?v=MBVSrM9MogI), [filling out forms](https://www.youtube.com/watch?v=IzhgvhB7nLE) and [sending forms](https://www.youtube.com/watch?v=WWEcbRkBwwA)
  * ViewWorld: Videos on how to [build a simple form](https://www.youtube.com/watch?v=Tuw9I_WZI7w), [export a XML form](https://www.youtube.com/watch?v=uDxYlR-T9L0), [build more complex forms](https://www.youtube.com/watch?v=7kTCMWXAfR0).
  * CartONG and UN Refugee Agency in Kenya and Serbia: [Deployment Manual](https://docs.google.com/document/d/1RjY_KImZbXZchyPeinLXXrqvm_laHzTVYK5yzl6kvPM/edit?hl=en#), [Training Slides](https://docs.google.com/present/view?id=dfzctfjq_419m5wsmgz), [Emulator Tutorial](https://docs.google.com/document/pub?id=18LbrTnyfJkG0CZDLMuVVzsU7ffNDnvzHJXEQ7poseuA), [Form Creation Tutorial](https://docs.google.com/document/pub?id=1SVryUoe2FFqqgFDudpGoEmFNJ2PBdT1_9k--Z7SXewA), [Other Tips](http://humanitarian-android.org/Main_Page)
  * Chris Kelley and RTI: [Setup Notes](http://www.ictedge.org/node/894)
  * Google Earth Outreach: [Tutorials](http://www.google.com/earth/outreach/tutorials/index.html#odk)
  * AfSIS Blog: [Deployment Notes](http://africasoils.net/labs/?s=ict4ag), [Training Guide](http://africasoils.net/labs/mobile/our-odk-training-experience-materials-included/)
  * Doug Browning: [Setup Notes](https://sites.google.com/site/dougbrowningportfolio/Resources/mobile-gis)
  * Chris Wilson: [Training Guide](http://blog.aptivate.org/2011/12/05/rough-guidehttp://wphostreviews.com/mappress-to-rural-data-collection-with-odk/)
  * Samantha Elghanayan: [ODK Collect and ODK Briefcase Starter Guide](https://groups.google.com/d/topic/opendatakit/Exx9EpusBiA/discussion)
  * Joe Doherty at CalGIS: [Mobile Meets the Cloud](/wp-content/uploads/2013/04/CALGIS-Mobile-Meets-the-Cloud.pdf)
  * Tania Bird: [Step by step for using ODK from start to finish](https://groups.google.com/d/msg/opendatakit/wxXDlVl83FI/gusIaaqdYooJ)
  * Jorge Durand Zurdo and ACF: [Online training modules and video](http://odk.acf-e.org/odk/start_here.html)

All contain great information and we recommend reading them all to determine what is most applicable to your scenario. If you have a training guide that you&#8217;d like to share, please email us <contact@opendatakit.org> and we&#8217;ll include it in this list.

## Notes from an ODK Field Project

_On the importance of properly training the enumerators to get good data using ODK, and on anticipating the many many things that can go wrong._

We (the UC Berkeley Human Rights Center) are working in the Central African Republic (CAR) on a social science research project concerning popular attitudes toward peace and justice. I may have mentioned this once or twice, but I am just making sure we are all on the same page.

This is the most recent in a series of projects in post conflict zones, The Congo, Uganda, Cambodia, etc. Because the same research group has completed so much research in the same area, we have established a methodology that is very effective. That is to say, we make good data.

Good data is the goal, ODK is the tool, and I would like to share some thoughts on the methodology for those of you who will plan and complete data collection in the field. You may find some of these things useful.

## Best Practices for Training

Most surveys are conducted with very little training. What happens is that a researcher, advocacy, or policy group realize that they need to answer a question. For example: How much food security does the population of Central Groovystan have? The researcher wants to know because he is writing a book about Central Grooovistan, the advocacy group wants to know so that when they are raising funds to feed orphans of the Groovystan wars they can give people an idea of how bad the situation is, and the policy group (Government) wants to know if their policy on import prices for Sorghum and wheat needs to be changed.

There are standard questions about food security: How much food of different types do you have? What percent of your budget goes towards food? This kind of thing. So, it is easy to put together an instrument, that is to say, a survey. The instrument is paper or electronic, it is basically a list of questions. The design of the survey instrument is an art in itself, we will come back to that at a later date. Take as given: We have a survey instrument.

Now, at this point, what usually happens is that the researchers will determine the sample size that will give them a meaningful measure of the question at hand. (more on statistics and sampling at another time) Let&#8217;s say that is is 2000. That means, if they sample 2000 people, and know the condition of their food security, they will know the food security of the population as a whole. This is called a representative sample. The have 30 days in which to collect data (for whatever reason), and they figure one Enumerator can do 10 surveys per day. 6 days a week, that&#8217;s 240 surveys per enumerator in the time allotted. You always need extra, because nothing ever goes right, so they hire 10 enumerators, and if they get their 2000 surveys ahead of schedule, everyone can go home to celebrate the biggest holiday in Central Groovystan, Groovemas.

What usually happens now is that they print up 2000 copies of the survey on paper and give them to the enumerators, who are told to go home and read it and come back on Monday for the start of data collection. No training at all. It&#8217;s just asking questions and writing down the answer, so it should be easy.

Nothing is easy, and nothing ever works the first time, and everything takes twice as long and costs twice as much as you think it&#8217;s going to, so there is no reason to think that this methodology will work.

In fact, even when we do research on paper, without ODK or anything, there is still training for the enumerators. In this case, since Central Groovystan is so groovy, they are doing their research using ODK on Android phones and there is no way they could do it without at least a little training anyway. No one doubts the need for software training, but it is important to use your training to solidify the methodology around ODK. Sampling, Consent, Interaction, Translation, Security, Confidentiality, and more all have a place in the training of enumerators.

For the research in CAR, we train for a solid week. 8 days really, so we get a solid 40 hours of instruction and practice. The first half of the training doesn&#8217;t even involve the PDAs, those show up for the last 4 days. With ODK, we can generate fake data in practice and analyze it after class so that we know if the survey forms are properly programmed, if the translation is correct, and if the methodology is understood by the enumerators.

So, here are some details on the process:

We are taken as a given here that the instrument (the questionnaire) has been properly designed, that sampling for statistical significance is complete and correct (you know how many people you want to interview), that is has been translated into your local language (French & Sangho!), and that your survey has been programmed into XML.

## Hiring Enumerators

You can train anyone, so don&#8217;t worry too much about finding people who are computer scientists and the like. Worry more about finding people with attention to detail, with a good work ethic. I will take a punctual enumerator over many other qualifications. Hire locally, there is no reason to transport people from afar.

Here in CAR, we need people who speak the local language anyway, it&#8217;s a strange tonal language called Sangho. That is the primary qualification. A good side effect here is that you are building local capacity and investing in the economy (write that in your grant application). We also look for people with previous experience doing surveys, if only because it takes a certain je ne sais qois to tramp around the countryside talking to strangers for weeks at a time. Some people think they might like it and they don&#8217;t.

We rely on a local NGO in CAR to do the hiring and logistics, so they handled this, but in the past, we have conducted interviews, lots of interviews, to find good candidates. Don&#8217;t settle for less, pay a rate that will attract a good group. This is Africa, so we are still only paying like $12-$15/day, I can&#8217;t remember exactly, but it&#8217;s a good wage and so we have 27 people, many of them with advanced degrees, computer experience, and survey experience. This is Africa, unemployment is like 40%.

Everyone should sign a contract, included in that contract are all the conditions of pay, per-diems, and conditions. Don&#8217;t be casual about this, otherwise you will end up renegotiating with people all the time. An example is that when you leave the city where people live, you have to sleep somewhere. Are you arranging the accommodation, or are you just giving everyone a fixed amount of cash to handle it themselves? Put it in the contract. Better yet, Make a contract with a local NGO to handle all of this kind of detail.

## Time and Space

Plan ahead, sufficient time to train the enumerators in sampling methodology, survey methodology, and using a handheld computer. (We usually refer to the Android as a PDA instead of a phone because the phone part of it is nothing but a distraction.) I think a week is good, but depending on the complication of your survey instrument, you may decide you need more or less. Even with 7 days of training, by the end, each enumerator will only have completed the survey from beginning to end half a dozen times.

Get a good room, with seats and desks and electricity. An overhead projector will let you project your Android Emulator on the wall and you will be able to demonstrate every function and button on the thing. At this very moment, I am in the Pope John Paul community center in Bangui, all around me are enumerators in pairs of two interviewing each other in the Sangho language and recording their data using ODK on Android handsets. There is a large grassy and tree lined courtyard where they can spread out and find a shady spot to sit for the lengthy survey. They can be outside to get GPS coordinates without getting hit by a car.

We want people to be here early and stay all day, so we pay them during training and we feed them breakfast and lunch. The day starts at 8:30, and everyone is here on time! We take a break at 10:30 for a croissant and a coffee. At 1pm or so, we have a nice African lunch.

In the room, the tables are arranged in a big horseshoe, the windows and doors are open so there is good light. Everyone has a paper name placard in front of them (they just write their name on a paper and fold it) so that we can all know each other&#8217;s names. Try and memorize everyone&#8217;s name. We have to work together for weeks and weeks, so let&#8217;s all be friends.

Note that you can only train so many people at one time. Of course, you are limited by the number of Androids that you own and can put in the field, but remember that you can&#8217;t effectively more than about 25 people at a time. 16 people is an ideal size group. There are logistics of room size, number of chairs, how much food can be provided, and if you are providing transportation, you can only fit so many people in a mini van.

Working in the field, we split into teams of 8 enumerators plus one driver plus one investigator. If you have three investigators, you can have three teams of 8 people in three mini-vans, so you can train 24 people at one time. There is no point in having more androids than that, but you might want to train a couple of extra people in case someone drops out, gets fired, or who-knows-what.

## First Things First

Start with the basics. Don&#8217;t even bring in the Androids for the first couple days. You want to get down to business so that people know what they are in for, so you can skip the philosophy, history, and theory. Break out the survey on paper and read through it together, out loud, from beginning to end. Let everyone take a question and go around the room, that way, everyone is involved.

Explain how questions are asked. The Enumerator is impartial, he/she must ask the question without passing judgment. The enumerator must not make interpretation of the answer. Get a straight answer, record it. Really, this is a learned skill. Before you ever got this far, you had your survey translated into local language and did several passes of translation, back translation. Hey, we found out that the first pass was all in the familiar tense when it really needed to be in the formal tense. You need to catch that kind of thing before training, but when you go through the survey in the local language, you will have a large group of people who might have something to say about fine shades of meaning and they can use this opportunity to familiarize themselves with the survey and improve it at the same time.

Also, it makes them feel a sense of involvement and ownership. Sango is an unwritten language. It can be written, of course, but there is not formal written Sangho, there are no Rules. So, people struggle to read their native tongue because it is the first time they have seen it written. A survey about peace and reconciliation has some high fallooting ideas in it, and translating that into a language that doesn&#8217;t have a word for &#8220;CD player&#8221; can be a challenge.

## Do Androids Dream?

Until everyone has familiarity with the survey questions and with the methodology of sampling and interviewing, do not break out the Androids. You will just confuse and distract people with your stupid gear. It&#8217;s not about the gear, it&#8217;s about the data. You get good data by asking good questions, so first, get to that point.

Now, break out the Androids. It&#8217;s exciting. You&#8217;re like a 50 foot santa claus with an elastic sack. Here comes a moment of fear. You are handing out dozens of pocket gizmos that are worth as much as people make in a year. You want to make sure you get them back. See above, the paragraph about hiring carefully.

To make sure that people take possession with an understanding of the gravity of losing these devices, we make everyone sign their Androids out at the beginning of every day and back in at the end. No one goes home with an Android. Use fingernail polish to number the chassis of every phone and assign the same phone to the same person everyday.

We lecture them on how important it is to never leave it lying around, never put it on the desk and walk away, even during training. Someone always forgets the first day and you will see a phone sitting on the desk, unguarded. Pocket their android and wait for the theft to be discovered. Then give them a mild and amusing tongue lashing in front of the whole class. It&#8217;s embarrassing for the enumerator, but you are saving someone the future embarrassment of losing one, because everyone will take it more seriously. You are saving yourself the embarrassment of explaining to your funders why you need to buy more Androids mid-survey. Give them soft slipcovers with neck straps so they can wear them under their shirts in the field.

## Giant Androids Crush Africa

Actual training on the use of the Android with ODK for data collection is pretty straightforward.

First, familiarize them with the hardware. Teach them to use the Android by going through all the hardware buttons and basic functions. Nothing is too simple to be explained, give people confidence so that when it comes time to take data it will be second nature. You will be well served to have a projector. Run the Eclipse Android Emulator so that you can show them how it&#8217;s done. Have one person running the laptop and another presenting. The presenter can interact with the projection like it&#8217;s a real Android, clicking on buttons and swiping the screen and the second person can run the emulator to create the illusion of a giant working Android.

Your enumerators should follow along with you and do a series of exercises so that they know what every button does and does not do and how to start and stop software and how to recover from errors. You want things to go wrong in training so that you can fix them. Treasure the challenge, your enumerators will screw things up in ways you could never think of, and it gives you the chance to train them to deal with it. It never occurred to me to worry about what to do when someone drops the phone and the battery flops out, crashing the whole survey. Even if the solution is to start all over because you lost your data, as long as you train people in this way, you have overcome the issue.

Turn it off, turn it on, crank the volume, hit the home button, put it to sleep, wake it up, swipe the screen, short press, long press, pop the keyboard up and down. Work that thing like a two dollar mule until everyone feels comfortable with it.

## Create an example form

Only now are you ready to ODK. I have a custom icon, and I clear all other icons off the screen, and as I am running Cyanogen mod, my home screen is five screens wide, I put the icon on every screen. There is no reason to make them open the apps panel and no reason they should ever suffer from lack of access to the program.

Do every step multiple times, and have the enumerators hold up their phones and show you the results. People don&#8217;t ask questions if they don&#8217;t have to, so interject yourself into their operation and help them on an individual level. It helps to have more than one teacher in the room.

Don&#8217;t use your real survey off the bat. I create an example form with each type of question, and some skip logic. It&#8217;s called Chaque Matin, which means Each Morning, and we use it every morning to warm up, and to get a good GPS fix for the day. You have to refresh your GPS almanac data so that you get a good fast fix when it&#8217;s time to do an actual survey. In the training, we use this form to warm up the crew.

Teach them to load the survey, my real survey is huge and never loads in less than 29 seconds, so it is good to have a small form for quick loading practice in the beginning. Use the projector and run through the form with everyone following along. Explain the difference between Text Input, Numeric Input, Single Choice, and Multiple Choice. Explain skip logic by example. Run through the example form several times. Take a break, have a croissant and a coffee.

Now, introduce the real form. Everyone already knows the form since they have already been through it on paper, so there is an air of familiarity. They already understand the use of the Android, so they are not all caught up in learning to swipe across the screen and pop the keyboard down when it blocks text.

## Exercise 1: The Roundabout

Everyone does a single survey together. Nominate one person to be the subject of the interview. Surely you have someone hanging around who isn&#8217;t training to use ODK. Each person takes a question in turn, everyone records the answer at the same time. It&#8217;s slow going, but you get everyone doing an interview together, so later, you can compare the surveys and see if everyone is recording the same answers.

There are some other benefits to this exercise.

  1. They get to parse the language together. You will improve the translation of the survey. Don&#8217;t let them get carried away splitting hairs. Not everyone will agree on wording.
  2. they get to practice pronunciation together. Very important, especially for unwritten languages like Sango.
  3. they find the errors in the skip logic and report them. I made so many errors in the skip logic. Why didn&#8217;t I find them myself? Because the survey is 300 questions long.
  4. everyone gets a feeling of community. They get to know each other and learn to support each other, they do part of your job by helping their neighbors when they are stuck.
  5. they get more familiarity with the survey.

During the exercises, be sure to wander around checking on individuals progress. Be patient, but don&#8217;t let them keep on making the same mistakes. Look for patters where everyone is doing the same thing wrong. Use these as teaching points.

Use what you learn in practice to improve your form, fix mistakes, and fine tune the translation.

## Practice, Practice, Practice

More exercises.

### Exercise 2: Self-Interview

The enumerators read the questions out loud to themselves and record the answers. It&#8217;s better than sharing interviews, because when you pair up in groups of two, you are really only training half of them. Half of them are just answering questions.

### Exercise 3: Paired Interviews

Let the enumerators pair up in groups of two. They can interview eachother. Sometimes, they can do alternating questions, switching back and forth. Most of the time, one of them should complete an entire survey as the interviewer, and then they should switch roles.

### Exercise 4: Almost the Real thing

Duplicate all the conditions of a real field survey, but in an area that doesn&#8217;t fit in your sampling. (so you don&#8217;t accidentally visit the same place later when you are doing real surveys) Let the enumerators follow the sampling selection process, go out into the neighborhood on their own, choose people to interview, and complete several interviews. This is the test of fire. Other than this being fake data, everything else should be just like the real survey will be.

Review the data from this exercise well. Look for things like the start and end times of the surveys. Are they so short that it might be fake? Look at the time between surveys. Is there enough time to do proper sampling? Look at the GPS coordinates. Are they in the same place? That would mean that your enumerator found a nice spot to sit down and completed a couple interviews without actually talking to anyone. Check the data to be sure they are answering all the questions.

It&#8217;s a good idea after this exercise to ask everyone to share their experience in class together. Some common problems will pop up, like failure of the subject to understand the questions, or confusion with the sampling methodology. This is when people realize for the first time that working in the field is not like practice.

## Murphy's Law

There are things I have notice that people tend to do wrong. Concentrate on training these bad habits away, or training them to be able to handle such problems with confidence.

Falling out of survey: It can happen that you close ODK in mid survey. Hitting the home button, then running some other thing, then hitting the ODK icon again. You might end up at the main menu again. In truth, usually you can hit the back arrow button and show up right in the same place you left, but the back arrow button can also exit a survey and present you with the close form without saving dialogue. It can be a little confusing. Train them to complete surveys, not mess around with the buttons, and if they fall out of the survey and end up somewhere else, in another application for example, to get back to the survey with a long press on the home button and then choosing ODK from the &#8216;recent applications&#8217; list. This seems to work well.

Skipping questions without providing an answer. Guys, you went all the way to some village in the jungle with the express purpose of asking this question, so don&#8217;t forget to record the answer! Just require all your answers in the Binding of the XML. Almost everything should be required. Sometimes there is no answer, so provide an option called &#8220;No Response&#8221;, then at least you are recording data. No Answer is still data. Failure to answer is not data.

Crash! If they are messing around and loading the survey and switching apps and going to the home screen, it can crash. Any app can crash. It&#8217;s not endemic, so I don&#8217;t think it&#8217;s an issue. Sometimes we encourage the enumerators to do some playing around in training, it lets them know there are limits. Use your Eclipse debugger to capture images of the error messages and show them to the class on the projector. Let them tell you what they are supposed to do when they see such-and-such an error.

Train them to bring issues to your attention, not just flounder around and start over. You need to know if your form is screwed up, or if you have found a new way to crash things.

Take phones away from people while they are working and pop up a menu or go to the home screen and give it back to them to see how they handle it.

## In Conclusion

Get good people and train them well. Take your time and try and think of things that can go wrong, then practice to get around those problems.

I hope this was some help to those of you who will be working on surveys using ODK in the future, and I invite comments and additions from those who have experience with training enumerators. Best of luck.

From Bangui,

Neil

## Appendix: Hardware Preparation

How to get the Android phones ready to be used as data collection instruments by field enumerators. These are the things I do to the Androids to prep them for use solely as data collection devices.

  * Uninstall old versions of ODK
  * Install the current version
  * Place the icon on the desktop
  * Remove all non-relevant icons and widgets.
  * Set the GPS to ON, WiFi off, data sync off, and destroy the widget. That way, no one can turn off GPS easily.
  * Set screen time-out to be long for training, short for the field
  * Airplane mode! saves battery.
  * Set Language to the native language of the enumerator
  * Turn off automatic orientation. Rotating the screen is no benefit in ODK.
  * Set the keyboard to be Touch Input and change the settings to remove all suggestions and spell checking. Turn off vibrate, turn on sound.
  * Calibrate the keyboard
  * Copy the current survey(s) to /sdcard/odk/forms using the Android Debug Bridge.
  * Load the form the first time to make sure it&#8217;s loaded, it&#8217;s valid, and save time later. It loads much faster the second time.
  * Get a Good GPS fix, the almanac can take a while to ready itself. The first time you use GPS in a strange place, it can take 20 minutes to load. Don&#8217;t make the enumerators do that. Getting a GPS fix on all the Androids updates the almanac data and the next fix in the same city will be way faster.
