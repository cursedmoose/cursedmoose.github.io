!---
layout: post
author: cursedmoose
title:  Hellbot Deep Dive - Making a Twitch Bot
date:   2022-11-08 13:00:00 -0800
category: update
---
Everyone should make a Twitch bot. Here's how.

While working in Amazon Games, the Twitch Crown Channel was looking to make their chat more interactive. They had a lot of good ideas that I should totally steal for a commercial Twitch Bot, but I'm having too much fun with AI hell to focus on that right now. Maybe you'll do it first. Anyway, after hearing this I immediately started researching how we could leverage a Twitch Bot to better track viewership habits, grant rewards, and manage chat features for anm expensive live production broadcast. I made a quick prototype, demo'd it, and then everyone got fired. Shit happens, experience stays.

## Step 1: Make a Twitch Bot
Twitch provides an [entire working example of a Twitch chatbot, absolutely for free, on their website.](https://dev.twitch.tv/docs/irc/example-bot/)

I am by no means a Javascript expert, but I managed to get it working and extend it to a few simple use cases. For Hellbot, I originally tried to copy what I learned into C#, until I found the incredible [TwitchLib](https://github.com/TwitchLib/TwitchLib) library. It's great. The C# package manager is great. Most of what you want to build is already built. You just have to wire it together and make it do what you want.

So hurry up, download [Visual Studio Code](https://code.visualstudio.com/) if you haven't already. Slam the code they provide into it and run it. Instant Twitch Bot. Instant gratification. 

Ok, spoilers, this took me probably 2-3 days to work through and understand the first time I saw it. There's a lot to learn.

## Step 2: Make your own Twitch commands


## Step 3: Learn to read an API reference (maybe this is next post?)
There two questions I ask myself whenever I'm trying to add functionality to a program:
1. Can I do it? (or, do the systems I need allow me to do it?)
2. How do I do it? (or, how do I leverage existing systems to do this?)

To answer both of these, we just need to look at the [API reference.](https://dev.twitch.tv/docs/api/)

The Twitch Bot example shows you how to receive and respond to command messages sent through the IRC chat client. Pretty neat, but there's not a ton we can do.