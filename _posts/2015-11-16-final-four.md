---
layout: post
title: Final Part Four - More Formal Project Plan
category: Physical Computing
---

<span style='text-decoration:underline'>Concept:</span>

It is becoming clear that with technological innovation in information gathering there seems to be no clear ethical boundary for what a state can or cannot do with regards to individual privacy. This type of surveillance implies the presumptive guilt of each citizen, and thus the burden of maintaining ones own privacy lies on the citizen herself. This is a fundemental problem and one that results in a unique type of anxiety that can only be felt by those who are being surveilled.

My idea for this project is to invert the gaze of surviellance in order to reproduce that unique anxiety for those on the other side of surviellance.

My proposal is to create a system in which Bill Bratton's privacy can be invaded at any given moment by people on twitter. I chose Bill Bratton because as the commissioner of the NYPD he represents an institution that exemplifies the type of power asymetry that is the subject of this project.

A camera will be placed strategically near the subjects house.  Whenever someone on tweets at a specific hashtag (still working on the hashtag), the camera will take a photo and send it to Commissioner Bratton as well as the the original tweeter.

Initially I considered having a remote server reach out to a Rasperry Pi Camera whenever a user tweets at it.  The server would then SMS the Pi Camera the username of the tweeter, and the Pi would respond with a photo (taken in real time) of Bill Bratton's house.  The limitation here is that if the Pi breaks or is confiscated, the whole project will be busted.  Instead I am considering a system that ensures greater longevity. 

Instead, on bootup the Pi will take a photo of B’s house every 5 minutes and send it to a heroku server. My heroku server will be doing two things: 
A) Running a script to listen for any tweets directed at brtncm. B).  Receiving and saving the photographs that my Pi sends it.  

Upon receiving a tweet, brtncm will respond by tweeting @commisionnerBratton and the original user the most recent image of B’s house. 

<span style='text-decoration:underline'>Milestones:</span>
<ol>
	<li>Seek legal advice</li>
	<li>Determine Correct Address</li>
	<li>Determine placement of camera based on legal advice and verified </li>address
	<li>Setup Raspberry Pi and Camera</li>
	<li>Write script to takes photos every 5 minutes and send to remote </li>server
	<li>Enable wireless (GSM or Wifi Dongle)</li>
	<li>Battery Powered Everything</li>
	<li>Write script to tweet when Pi boots up so that you know if it is </li>working
	<li>Create scraper/tweeter</li>
	<li>Source quotes</li>
	<li>Fabricate camera</li>
</ol>

<span style='text-decoration:underline'>Technology Specifics</span>

This <a href = 'https://www.adafruit.com/products/1566'>Battery Pack </a> 
will supply me with 15 hours of battery.  So I will have to recharge the camera every day.

The other option is to use solar energy to power the Pi. I would use <a href="http://www.voltaicsystems.com/blog/powering-a-raspberry-pi-from-solar-power/">this tutorial</a> as a guide.  Unfortunately, given time constraints, I am worried that I won't have time to create a fully solar based solution for powering my pi.  I'll have to do some more research.

As for getting on to 3g I have found a few options. <a href="https://content.konekt.io/blog/raspberry-pi-on-cellular/"> I could buy a Sim Card.</a> Or I could consider setting up a wireless hotspot.

	
<span style='text-decoration:underline'>User Types</span>

Activist/Protestor: This is the target audience of the application.  The activist already knows who Bill Bratton is, and is interesting in engaging in a gesture against police surveillance. This activist will send a tweet to brtncm and receive a photo or B’s house. Included with the photograph will be a relevant quotation from the subject.  The Protestor/Activist should be motivated to tweet multiple times for the purpose of antagonism/citizen monitoring/ dedication to the idea.  Ideally the activist will share the tweet with her friends.

Troll: The troll hears about this idea through social media or a friend and is interested in sending antagonizing, anyone for the sake of antagonism.  The troll will be motivated to use this interface by her conviction to the idea of antagonism.  Likely she will not share her tweets.

Casual: A casual user heard about the btrncm from a friend or from social media.  She does not know too much about Bill Bratton but tweets at the hashtag to see what happens.  When she is presented with a photo of someone’s house and a quote, she investigates the twitter user and discover more information about Bill Bratton.  She only uses the tool once and likely will not share her experience.  But she will learn a bit more about the commissioner. 

Friends/Family:  These people will just tweet at brtncm because they like me. Depending on how much they like me, they’ll do it twice. 


<span style='text-decoration:underline'>Timeline:</span>
	
11/18: Solidify Concept and Tech.

11/25: Have ordered all necessary parts for initial prototype and have completed milestones 1 - 5.

11/2: GSM enabled and initial prototype with battery power.

11/9: Fabricated.


