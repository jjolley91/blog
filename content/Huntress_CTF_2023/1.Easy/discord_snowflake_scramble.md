---
title: "Discord Snowflake Scramble"
date: 2023-10-25T13:11:20-10:01
#draft: true
tags: ['CTF','Writeups', 'Misc', 'Easy']
---

# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Easy Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/welcome_to_the_park)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/blackcat)

### Someone sent message on a Discord server which contains a flag! They did mention something about being able to embed a list of online users on their own website...

### Can you figure out how to join that Discord server and see the message?

Here we are given this link to discord: https://discord.com/channels/1156647699362361364/1156648139516817519/1156648284237074552

In Discord, a "snowflake" is a term used to describe a unique identifier for various objects within the Discord platform. These objects can include users, messages, channels, and more. Discord uses snowflakes to ensure that each object has a unique, timestamp-based identifier, making it easier to manage and track different elements within the platform.

A Discord snowflake typically consists of the following components:

A 41-bit timestamp: This represents the creation time of the object, down to the millisecond.

A 10-bit machine identifier: This identifies the machine or worker responsible for generating the snowflake.

A 12-bit sequence number: This distinguishes different objects created within the same millisecond.

The combination of these components creates a unique identifier for Discord objects, ensuring that no two objects created at the same millisecond on the same machine will have the same identifier. This is useful for tracking and managing objects, such as messages, in a distributed and scalable system like Discord.  

To solve this we need to understand how discord snowflake ids work. In the url, the first number is the guild/server id, the second is the channel id, and the third is the message id.   
Here is some info on [Discord Snowflake IDs](https://discordlookup.com/help), and we can also use this site to discover the discord server name using the server id.  

![discord_snowflake2](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/discord_snowflake2.png?raw=true)

Then all we need to do is join the server, and retrieve the flag!

![discord_snowflake](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/discord_snowflake.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/welcome_to_the_park)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/1.easy/blackcat)