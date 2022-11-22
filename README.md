# How To CTF

Welcome to the fantastic world of Capture The Flag events! These are the perfect chance to hone your Cybersecurity skills and put them to the test. This guide will go over everything you need to know before partaking in a CTF.

## What is a CTF?
A Capture The Flag event is usually comprised of multiple challenges where the aim is, as the name suggests, to find the flag, individually or in a team. The flag is usually a string of text following a specific pattern, so make sure to read the event's instructions to find out what the format is!

Here's an example!

![Example Flag Image](https://github.com/Vintrae/How-To-CTF/blob/main/images/flag_sample.png "Example Flag Image")

## Types of challenges

CTFs sometimes focus on a single category of challenge, but it is more common to find challenges belonging to multiple categories so participants can choose what to tackle. Some of the most common categories are:

### Cryptography
Cryptography is the practice of securing communication by making the data incomprehensible to the parties that aren't meant to access it. Thus, cryptography challenges tend to offer a file or sample binary that contains the information. The key is finding what method has been used to obfuscate the flag and figure out a way to extract it. Make sure to read on cyphers if you want to tackle this category!

### Web Exploitation
This is one of the broadest categories in CTF challenges, but usually revolves around gaining access to a web service to reach the flag. This is usually achieved by exploiting a vulnerability in the service, the server it sits on or the protocol it uses to communicate. Page source inspection, SQL injection and cross-site scripting are your friends here.

### Steganograpy
This fun category is all about hiding information in plain sight. The player is usually given a file that contains the flag and have to figure out how to extract it. The given file could be an image or even an undefined type of file... often times things are not what they seem here! Brush up on EXIF data, magic numbers and image editing if you want to dive into these challenges.

### Coding
A very beginner-friendly category that will test your coding skills. Are you a fan of automation of repetitive tasks? This is the place to be for you. The flag may have been compressed a thousand times or perhaps you have to beat a game that needs you to click hundreds of times per second! You'll have to outsmart the machine to get the prize.

### Reverse Engineering
If you want to deep dive into binaries and feel the urge to incessently look at lines of Assembly code, look no further. These challenges provide a binary executable that could, for instance, ask for a password from the user. The goal is the disassemble the piece of software to understand what the right input is that will give out the flag.

Now that we've had a look at the different categories, it's time to get started! Feel free to explore the categories in any order, according to your interests. There are also many different categories that haven't been mentioned here, so come back to this wiki at any time to get more information.

## Getting started
If you do not know where to start, our recommendation is you read our Linux guide. It will give you some basic understanding of some Linux tools and commands that will come in handy in your journey.




