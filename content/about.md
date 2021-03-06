gay-psotnic is a fork of psotnic 0.2.14 which has been developed from 2009 to 2010 as a private version.

## Changelog
```
features
--------
- multiple listenports
  - can be for "all", "users" or "bots"
  - example conf entries:
     listen 127.0.0.1 9000 all
     listen ::1 9001 all
     listen ssl:0.0.0.0 9003 users
     listen 0.0.0.0 9004 bots
- allow bots to link over ipv6
  - hint: use .+addr <bot> <ipv6>
- improved partyline:
  - partyline must be joined by irc client, e.g. /SERVER [-4 | -6] [-ssl] <hub-ip> <hub-port> <ownerpass:username:userpass>
  - show syntax errors
  - .help <command> shows syntax (further descriptions may follow)
  - added .bc <bot> help
  - added timestamps to all lines in partyline
  - allow to join partyline of slave/leaf by telnet or dcc, requires that ownerpass is set
- multiple ownerpasses can be used
  - they can also be added by: .bc <main> cfg +ownerpass <password-in-plaintext>
- resolve hostname of main/slave before linking, requires adns
- resolve hostname of irc servers before connecting, requires adns
- added 'ipv4:' and 'ipv6:' prefixes to class entHost, example: +server ipv6:localhost
- new channel mode management, use chars instead of static FLAG_*, same for sent modes
- new mode-lock
- implemented raw command: .bc <bot> raw <text>
- global and local +n can do .+user, .chanset, .mk, .bc <bot> cwho/names <chan>
- global and local +n can change channel flags of users who do not have +n too
- .+/-addr <handle> <ip4/6> allows that user to join partyline only from this ip (cidr is supported)
  - must be used for bots too
  - removed telnet-owners
  - please do not use .chaddr anymore!
- report connecting errors also when the bot was not registered on irc
- show maximum size of core file in .bc <bot> status
- added .set resolve-users-hostname which will tell the bot to resolve all hostnames of users
  who join or are already on a channel, needed for clonecheck (off by default)
   issues: - when bot connects to irc and joins channels it will resolve very much hostnames,
             same after netsplit
           - every bot resolves the hostname on its own, why don't they share the work
           - not very useful in the end
- changed password set behavior on irc (requested by AnGelZ):
  - must be enabled by .set allow-set-pass-by-msg
  - slaves/leafs can set passwords too unless the user has +xsnm and unless the user had no password set before
- leafs can save the userfile too, cfg: save-userlist ON
- implemented calculatePenalty() of "raw" module
- leafs can link to main
- added myipv6 cfg variable
- make install (thanks to [C]167)
  - ".bc <bot> update" should always work now
- warn on partyline if *.dec or seed.h was found
- clear beIR list when it is full
  - channel will be locked during the process if lockdown chanset is on

bug fixes
---------
- fixed SSL problem which caused high cpu load (#1906516)
- chanuser::updateDNSEntry() does not resolve ipv4/6 addresses anymore
- .set takes the whole string as value and not only the first word (reported by anank)
- buffered data of net.hub and net.irc has not been sent
- restart did not work if config was opened with fd=0

misc
----
- renamed +/-shit to +/-ban
- -ban/exempt/invite/reop takes channel as first parameter (as +ban does)
- set default value of resolve-threads to 1
- checkKeepout(), checkModelock() and checkList() will only be executed when necessary
- split parse-owner.cpp into functions
- renamed parse-owner.cpp to partyline.cpp
- removed bold text from partyline
- removed inet::sendCmd()
- removed oidentd spoofing support, added "oidentd" module
- removed anti-idle and away feature, maybe a module will follow
- removed support for cisco routers
- removed support for bnc (only bnc from gotbnc.com was supported)
- removed socks5 support and jump5 command
- removed incomplete tcl support
- removed shit-last-used
- removed takeover mode
- removed critical lock
- removed .chnick
  alternatives:
  - .bc <bot> raw NICK <newnick>
  - if keepnick is enabled: .bc <bot> cfg nick <newnick>
- removed entChattr class
- removed "make static"
  - added ./configure --disable-modules
- merged chanset "channel-ctcp" and cfg "private-ctcp" settings to "reply-to-ctcp" cfg setting
- renamed rejoin-delay to rejoin-after-kick-delay
- renamed auth-time to auth-timeout
- rewritten inet*::*send(), client::privmsg(), client::notice()
- replaced sendOwner() by sendUser() in most cases
- replaced .rdie by .bc <bot> die
- replaced .restart by .bc <bot> restart
- replaced .names by .bc <bot> names <chan>
- replaced .cwho by .bc <bot> cwho <chan> [v|o|l|b]
- replaced .update by .bc <bot> update [id:pw]
- replaced .stopupdate by .bc <bot> stopupdate
- replaced .rjump/6 by .bc <bot> jump <#number of server> (see .bc <bot> cfg server)
- replaced .status by .bc <bot> status
- "make" points to "make dynamic"
- +ban does not show handles in kickreason anymore
- moved kickreason, limitreason, keepoutreason, partreason, quitreason and cyclereason cfg settings to userlist (.set)
- renamed limitreason to limit-kickreason
- renamed keepoutreason to keepout-kickreason
- added clonecheck-kickreason
- configure checks if ssl is supported
- main-bot reports if its hostmask is not added when an owner goes to partyline
- bots join channels even if their hostmask is not added
- changed almost all quitreasons to the one defined in .set
- check if a joining user is in channel banlist (requested by matrix)
- ctcp hook works also if reply-to-ctcp is off
- rewritten lag check for irc:
  - replaced ISON check by PING
  - current lag is displayed in .bc <bot> status
  - new variable: .set lag-check-time
  - set conn-timeout to 5m
- ".list d" became a remote command since it did not work well
- client::privmsg() and client::notice() put msgs in a queue
- report on partyline if bot cannot register because of an erroneous nickname
- creation mode does not give +a flag anymore (requested by matrix)
- try to set core file to unlimited
- removed "Autosaving userlist" notice
- removed lagcheck from "repeat" module, uses psotnic's lagcheck now
- updated config creator
- report resolving errors on partyline
- removed ./psotnic -c and -p - please use ./psotnic -n or -ne (expert mode) instead
- ignore "CAP LS" sent by irc clients during login
- psotnic -n creates an owner account
  - removed all other ways
- added auth support to update function (.bc <bot> update [id:pw])
- removed DCC CHAT feature, added "dccchat" module
- introduced timestamp for userlist (not used yet)
- new definition of leaf: leaf is what does not listen for bots
- show if module support is enabled in .bc <bot> status
```
