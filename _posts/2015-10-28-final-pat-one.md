---
layout: post
title: Final Part One
category: Physical Computing
---


Over the last year I have been becoming increasingly more concerned with the future of privacy.  I attended a conferance two weeks ago at Bard in which Edward Snowden, amongst many other speakers, stressed the ethical importance of technology producers and artists to fight to maintain privacy for themselves and others.  In a class I am taking about surveillance, we are learning about more and more aggressive approaches to information gathering and population control that the State employs. 

It is becoming clear that with technological innovation in information gathering there seems to be no clear ethical boundary for what a state can or cannot do with regards to individual privacy.  This type of surveillance implies the presumptive guilt of each citizen, and thus the burden of maintaining ones own privacy lies on the citizen herself.  This is a fundemental problem and one that results in a unique type of anxiety that can only be felt by those who are being surveilled.

Ben Wizner of the ACLU sums this idea up wonderfully in a rhetorical question he often poses: "How do you feel when a police officer pulls up along side of you?"  

This is a unique anxiety that is caused by a gross asymetry of power and a constant state of presumptive guilt.  

My idea for this project is to invert the gaze of surviellance in order to reproduce that unique anxiety for those on the other side of surviellance. 

My proposal is to create a system in which Bill Bratton's privacy can be invaded at any given moment by people on twitter.  I chose Bill Bratton because as the commissioner of the NYPD he represents an institution that exemplifies the type of power asymetry that is the subject of this project.

My plan is to scrape twitter in real time for tweets regarding our commissioner and then tweet a photo (in real time) of his house back at the original sender. 

Using Twitter's Stream API, I will run a script on a remote server that listens for tweets.  Upon recieving one, I will record the username, and ping a remote camera that is located in a strategic location.  The Camera will take a photo and send it back to my server, and I will tweet the photo back to the original tweeter.  

I imagine I will need a SIM card for my arduino or raspberry pi in order to make a connection to a remote server without internet.





