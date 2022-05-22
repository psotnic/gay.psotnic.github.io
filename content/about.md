---
title: "About"
permalink: "/about/"
layout: page
---
Psotnic is an [IRCnet](https://www.ircnet.com) bot written in C++. The main goal of the project was to create a fast, stable and easy to use bot.

Here is a list of features:

* antiidle
* 7 ctcp emulation types
* kick4 and kick6
* ipv6 support
* clone check: host, ident, /24 ipv4 class, /64 ipv6 prefix, proxies (*!~*@*.isp.com)
* socks5 support
* vanilla BNC support
* shitlist (shits are enforced upon addition)
* alternative slave support
* module loading (each one is protected with md5 sum)
* 3 types of owners (permanent (+x), super owner (+s), owner (+n))
* channel modes protection (only +n can change channel modes)
* master can only op one person per mode
* encrypted links between bots (blowfish)
* encrypted config file and userlist (blowfish)
* autolimit
* limit override protection (mass invite protection)
* ban and limit enforcing
* user level based protection (user gets kicked if he harms user with higher level)
* mass, remote and slave joins
* channel flags support
* dynamic invites, bans and exempts
* was op test
* keepnick
* no trust between bots
* very fast oping (does not use botnet for oping) algorythm
* getop (nearly not used for oping), getkey, getinvite, unban
* all features can be controlled via .set and .chset command
* channel locking (+i) when number of bots on channel reaches below critical level
* CIDR ban support
* bots can be updated via partyline
* 15 chars long nicknames support
* reop (+R) mode support
* on join host resolver (linux only, since 0.2.3)
* config can be edited via partyline (since 0.2.3)
* omnipresent hashtables make bot less cpu consuming (since 0.2.3)
* new random number generator makes (xor shift) decision algorithm less cpu consuming (since 0.2.3)
* source code (since 0.2.6)
* ident spoofing for oidentd (since 0.2.8)
* SSL support for irc and partyline connections (since 0.2.9)
* partyline management of invite, exempt and reop modes. (since 0.2.12)

There are a lot of more features. Please read the documentation and the changelog.
