---
layout: post
author: cursedmoose
title:  Hellbot Deep Dive v1
date:   2022-11-08 00:00:00 -0800
category: update
---
A brief overview of how Hellbot started.

It's been a while since I've written anything technical, so I figured I'd capture what the motivation for Hellbot was, where Hellbot is now, and what I'm looking to do in the future.

## Motivation
In Mid 2020, GPT-3 was starting to make the headlines. After stumbling across [AI Dungeon](https://aidungeon.com/), the opportunity of making a shared, interactable narrative became clear.

I was working in Alexa at the time and tried to leverage the idea for kids' stories but didn't get any traction. Oh well, [they finally got there.](https://www.theverge.com/2023/9/20/23880764/amazon-ai-alexa-generative-llm-smart-home)

In mid-2022, Generative AI became the hot new thing. With the services like the new ChatGPT model and Midjourney image generation going mainstream, the possibilities (and horrors) of AI generated content quickly became reality.

After stumbling across [Nothing, Forever](https://www.twitch.tv/watchmeforever), I started imagining a hellscape of an infinite number of shows and channels creating infinite generated content, such that every niche could be fulfilled. I was terrified, and eager to try my hand at it.

## Early Stages - Imitation
The [Dagoth Ur voice acting mod/meme/etc craze](https://www.pcgamer.com/modders-are-using-ai-to-put-voice-acting-in-morrowind-and-im-impressed-and-concerned-all-at-once/) was the first thing I considered buying into.

With ChatGpt3's generally bad, rambling prose, I saw an opportunity to make an infinite Twitch stream of an AI-powered Dagoth Ur spouting blasphemy to all that wish to hear it. The idea lives on in the form of the Dagoth Ur TTS you will sometimes hear on the Stream, and the AI-powered blasphemy, now voiced by Sheogorath.

## Early Stages - An Actual Use Case
In early 2023, I was working on a team in Amazon that specialized in playful experiences. We got wind from the Crown channel that they wanted more ways to engage their audience without waiting for Twitch to roll out features. In the initial pitch and planning for this, I finally found out what it took to create a Twitch Chat bot. 

Turns out, not much! 

While that project never got off the ground (mostly due to the layoffs), I had so much fun thinking of ways to interact with chat that I turned it into a personal project. Hellbot was born. 

## Hellbot, v0
Inspired by the ever-popular TTS options that Twitch Streamers used, but bored with the lack of variety, I started with two ideas:
1. Allow Twitch viewers to create their own TTS voice, which plays when they send a message in chat.
2. Have an AI respond to those messages and interact with chat, creating a 3 way dialogue between myself, chat, and an AI. Chaos.

While the second idea still mostly eludes me (but inches ever closer with speech-to-text apis), the groundwork for Hellbot was ready.

Leveraging a simple Twitch Bot implementation hooked up to OpenAI and ElevenLabs APIs, I created the initial version of Hellbot. It didn't do much, other than play some users' chat messages in TTS and occasionally say random things in Sheogorath's voice, but I loved it. Streaming can be a lonely experience and being able to hear other people's voices has made it a ton more fun for me.

## What next?
Stay tuned for some additional blog posts where I go into other integrations and talk about the product motivations and tech solutions.