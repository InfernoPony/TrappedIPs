# TrappedIPs
A not-often-updated list of IPs that have triggered one of my IP scanner traps

## What is this?
I maintain multiple servers around the globe. Some are connected directly to the internet, while others are on private networks.  
When you go on the interwebz, you're in the middle of the battle field. You will find friendly people wondering what they're doing here, but also dangerous enemies you'll want to avoid at all cost.  
Once my servers where online, I quickly found out that scanners usually belong to the second category. Some of them will tell you it's for research purposes, some will say "we're just knocking on the door a see if someone answers", some won't even try to explain themselves, ...  
But no matter why, the fact remains: they try to scan the entire web to see what's available.  
Listing public content is one thing. Companies like Google do this very well. But the fact that a server is reachable doesn't mean that it is meant to be public. Just because you have a chair in front of your house and no electrified fence around your property doesn't mean anyone can spend the day sitting on it or go home with it.

Even if some of them have no malicious intents, I'm not gonna do a background check on all of them. I already have a 1000+ list and no time to waste on that.  
So I chose a different solution: I set up traps, list all IPs that try to access them, and add them to a blacklist.  
And since I'm probably not the only one tired of mass scanning, I'll make my blacklist publicly available.

## How do you decide if an IP is trying to scan your servers?
Very easy : on internet-facing servers, I usually use a very restricted list of ports.  
Let's say I run a FreeBSD web server. It should listen on ports 22, 80 and 443. But there is no reason to listen on port 25.  
So, my web servers will consider port 25 as trap. And SMTP servers will consider port 80 as a trap...

My nftables rules contain this line: `tcp dport @trap_scanners_v4 add @blacklist_scanners_v4 { ip saddr }`.  
Try to access a port listed in the `trap_scanner_v4` set and you'll be added to the blacklist. The lists from multiple servers are then merged and redeployed on all nodes.

## Is it exhaustive?
No.  
Since some of my servers can only be managed via SSH or RDP, and I don't want a mistake to ban me from my own servers, I don't check all ports. In fact, I only check 2 or 3 ports on each server.  
I know lots of scanners will be ignored, but I also know it's an endless war. No matter how hard I'll try, I won't be able to list all scanners.  
However, I can at least reduce the number of scanners that can successfully collect data from my servers.

## What about research?
If a scientist tried to enter your home "for research purposes" without asking for permission first, what would you do? Offer him a coffee while he checks your family photos, or call 911?

## I'm in this list!
So you're admitting you tried to scan my server? Then you belong to this list.

## So you won't remove a single IP from this list?
I might eventually remove some of them, but don't have too much hope.  
IPs in this list are here because they fell into a trap. There are very few reasons for me to remove an IP from this list, and I won't make a public list...

## How often is the list updated?
This repo is sometimes (and I insist on **sometimes**) updated with the latest version of the blacklist.

## So... I can use this list for my own firewall?
I wouldn't make it public if I didn't want people to use it...

## How can I be sure those are actual scanners?
You can't.
Trust me or not, but don't expect any proof. There is no way for me to prove that all those IPs have actually tried to scan my servers.  
I don't even keep logs , so I can't tell you when they did or what else they tried. And had I logs, I wouldn't provide them since it might allow a scanner to identify my traps...

## I run a scanner, but I don't wanna end up on this list!
Then don't scan my traps.  
Wait, you don't know what to exclude? I'd advise you to try 0.0.0.0/0...

## License
This repo is under the Beerware Licence.  
Want to learn more? Check https://en.wikipedia.org/wiki/Beerware
