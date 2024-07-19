---
title: "Safe for skin safe for emails..."
date: 2024-07-01T13:11:20-10:01
tags: ['CTF','Writeups','Email_Security','Warmups','Easy']
---


# [Home](https://jjolley91.github.io/blog/) >

###  [Cyber Defense CTF](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/) >  [Email_Security](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Email_Security/)

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Email_Security/identity_crisis)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Email_Security/out_phishing)

### I keep more than your skin safe. 😃

The answer is spf. 

SPF, or Sender Policy Framework, is an email authentication protocol designed to detect and prevent email spoofing. It works by allowing domain owners to specify which mail servers are authorized to send email on behalf of their domain. Here's a more detailed explanation:

How SPF Works:
1. Domain Owner Sets Policy: The owner of a domain publishes an SPF record in their DNS (Domain Name System) settings. This record contains a list of IP addresses or hostnames authorized to send email for that domain.

2. Email Sent: When an email is sent from a domain, the receiving mail server checks the SPF record of the sending domain.

3. SPF Check:

	* The receiving mail server looks up the SPF record of the sending domain in DNS.
	* It compares the IP address of the server that sent the email to the list of authorized IP addresses in the SPF record.
4. Result:
	* Pass: If the sending server's IP address is in the SPF record, the SPF check passes.
	* Fail: If the IP address is not listed, the SPF check fails.
	* Neutral/None: If there is no SPF record or the result is inconclusive, it can return a neutral or none result.

5. Action: Based on the result of the SPF check, the receiving server can take appropriate actions such as accepting the email, flagging it as suspicious, or rejecting it outright.

## [Back](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Email_Security/identity_crisis)  <> [Next](https://jjolley91.github.io/blog/level_effect_cyber_defense_ctf_2024/Email_Security/out_phishing)