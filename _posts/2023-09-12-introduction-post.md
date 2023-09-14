---
layout: post
title: Thomas's Epic Battle with Ruby
author:
- Thomas Moslander
---
# It's Finally Here!

My first blog post! Wow! What a journey I've been on to make it this far. Let me give you a little context before we dive into what I've been through to make it here....

## The Big Crash (and the reinstallation of Windows 11)

Picture this: it's the spring semester of 2023. I'm taking Operating Systems and Concurrency with Dr. Ferrer, and I schedule an office hours meeting to deal with what was *surely* just a teensy tiny problem: Windows Subsystem for Linux was supposedly and allegedly installed, but it wouldn't let me choose Ubuntu as the distribution. Surely that was just a simple fix, right?

*Right?*

Well, let me tell ya, it was most assuredly **not** a simple fix. In fact, it wasn't ever actually fixed. Dr. Ferrer and I fought bravely, but in the end, we had to surrender (and delete + reinstall the entirety of Windows 11 on my machine in the process. It was not a fun two hours.)

Ultimately, I went to Best Buy and bought a whole new machine: a Mac. I thought *surely* that would be the end of my woes with different OSs since now I had both a Windows machine and a Mac machine. But, *oh*, how wrong I was...

## A New Challenger Approaches: Ruby!

I started off attempting this lab on my Mac machine, since I'm used to using it more often than my sometimes-questionable (okay, maybe often-questionable) Windows machine. But man, did I run into loads of problems! Here's a play-by-play of the most crucial moments:

1. bundle install
Trying to run "bundle install" resulted in this error message: 
*"Your RubyGems version (3.0.3.1) has a bug that prevents 'required-ruby-version' from working for Bundler. Any scripts that use 'gem install bundler' will break as soon as Bundler drops support for your Ruby version. Please upgrade RubyGems to avoid future breakage and silence this warning by running 'gem update --system 3.2.3."*
There were also lots of *"retrying download gem"* messages, before it gave up and spat out another error message:
*"Bundler::PermissionError: There was an error while trying to write to '/Library/Ruby/Gems/2.6.0/cache/public_suffix-5.0.3.gem'. It is likely that you need to grant write permissions for that path."*
Okay, well, let's try this next:

2. gem update --system 3.2.3
But trying to update led to this error message:
*"You don't have write permissions for the /Library/Ruby/Gems/2.6.0 directory."*
Huh. Luckily, we live in the age of the Internet! I found [this](https://stackoverflow.com/questions/51126403/you-dont-have-write-permissions-for-the-library-ruby-gems-2-3-0-directory-ma) StackOverflow question, and I got to work messing with chruby and ruby-install. But I was *still* experiencing trouble, which brings me to my next attempt:

3. \curl -sSL https://get.rvm.io | bash -s stable
This command was actually successful! Yay! But unfortunately for me, running "bundle install" still gave the same error message. It was time to try something new.

4. brew install ruby-build and brew upgrade ruby-build
Another successful command! But another unsuccessful "bundle install" run.

5. gem install rubygems-update
This command gave the following error message:
*"While executing gem...(Gem::FilePermissionError) You don't have write permissions for the /Library/Ruby/Gems/2.6.0 directory."*
Time to try something new!

6. update_rubygems
This was an unfound command. Moving forwards!

7. \curl -sSL https://get.rvm.io | bash
This command was successful! But "bundle install" was still unsuccessful.

At this point, I was pretty thoroughly stumped. I had tried seven different approaches to this problem, half of which I had found on some obscure corner of StackOverflow without actually understanding what they were doing to my machine. (Don't be like me!) Oh, where to turn in such a dark moment!

And that's when it hit me: *Dr. Goadrich*!!! Dr. Goadrich would be able to help. So, I set to sending perhaps the longest Teams message I have ever sent, detailing all of my attempts and the errors they resulted in. 

And he had an answer! 

- sudo gem update --system 3.2.3

And it seemed like this command made some progress! It still generated an error message, but it was generating a *new* error message. And, by this point, I would take any form of progress!
*"While executing gem...(Errno::EPERM) Operation not permitted @ rb_sysopen - /usr/share/man/man1/bundle-platform.1"*
It was pretty hard to decipher just what, exactly, this error message was trying to tell me. But Dr. Goadrich would have an answer!

...Except he had *never* seen that error message before. (What?! My professor *isn't* actually an all-knowing, oracle-esque expert at everything computer science?!) That meant this was **serious**. I had to be on my guard-the last time a professor was stumped by my somehow always cursed machines, we had to delete and then reinstall the entirety of Windows 11. I was determined not to let Ruby get the best of me after Ubuntu had so thoroughly destroyed me last semester. I would not falter in my moment of redemption after last semester!

And, thankfully, Dr. Goadrich was not completely unprepared! Being the awesome professor that he is, he had something he had found for me: a *link*! 

- [Dr. Goadrich's link](https://stackoverflow.com/questions/32891965/error-while-executing-gem-errnoeperm-operation-not-permitted)

It seemed the heart of the problem lay with Mac: there was a new security feature called **System Integrity Protection** that was stopping me from modifying certain files. I had two options:

1. Option One: sudo gem install -n /usr/local/bin
Option One was unsuccessful. My only chance was Option Two:

12. Option Two: **Disable** SIP.

It was a pretty simple process, laid out in four steps, but I was hesitant. Did I really want to mess around and disable something like that on my machine? 

Ultimately, I knew what had to be done. There was never any decision to be made, because it was already made in my mind before I even read what the four steps were. I knew what the path that lay ahead of me contained....

## Returning to my Roots (or my Windows 11 Machine)

I busted open my old Razer laptop and got to work. It was time to face Ruby once again, and to come out the other side victorious with a super awesome blog post detailing the long fight against my new enemy.

It was a long hour or two in the library tussling with Ruby, but **I did it!** I won! **I fought Ruby and I won!!!**

And now, here we are. Undefeated, redeemed, and writing a super awesome, maybe slightly too long blog post about it. Here's to hoping this redemption arc and era of victory lasts throughout the semester!