class: center, middle, inverse
# capture the flag
[learning through competition]
.footnote[View source on [GitHub](https://github.com/audibleblink/ctf-talk)]

---
layout: false
class: center, middle

# Sometimes you win, sometimes you learn
.footnote[-- Abraham Lincoln, probably.]

---
class: center, middle, inverse
# Getting Started
### [[Understanding](#) How You Learn]

---

.left-column[
# What is it?
]

.right-column[
# A collection of challenges designed to test skill.
.paragraph[
- Reverse engineering
- Webapp Exploitation  
- Crypto  
- Forensics  
- Exploitation  
- Steganography  
- OS / Network  
]
]

---

.left-column[
# How do I win?
]

## Flags are trophies that prove you've completed a challenge.
.right-column[

```
FLAG{d41d8cd9e980fuo0998ecf8427e}
CTF{y0ur3_s0_1337_u_f0unD_tHe_fl4g}
# or whatever the CTF rules say the flag format is
```

.paragraph[
- Documents
- Cracked Passwords
- Logs
- Database Tables
- Network Packets
- Audio Files
- Metadata
]


]

---
class: inverse
# Test Case  | __asciinema__

<a href="https://asciinema.org/a/110084?t=20" target="_blank"><img style="width: 100%; " src="https://asciinema.org/a/183006.png" /></a>

---

.left-column[
# Different Learning Stages

------

## Test Case: 

##IDOR on asciinema.org
]

???
## Example problem: IDOR on asciinema

#### Answers First
If I get absolutely stuck, I come here

#### Basics

Learning the HTTP Spec

There's always time to come back and learn this.
In fact, you'll need to if you want to 'LEVEL'

#### Practical Application First
This one is me. I want to learn things that help
me solve problems directly in front of me.

--
.right-column[
### Answer First?
]

--
.right-column[
```sh
1| base='https://asciinema-bb-eu.s3-eu-west-1.amazonaws.com'
2| endpoint='/uploads/asciicast/file/_/ascii.cast'
3| key='?AWSAccessKeyId=xxxx'
4| for id in $(seq 10000 99999); do
5|   uri="${base}${endpoint/_/$id}${key}"
6|   curl -sL "${uri}" >> dump.loot
7| done
8| 
9| grep 'FLAG{' dump.loot
```
]


--
.right-column[
### Practical Application First?
Locate from where asciinema pulls the playback information and locate sensitive data
]

--
.right-column[
### Basics First?
]

--
.right-column[
* RFC 2616  -  Hypertext Transfer Protocol
* [REST] Roy Fielding's dissertation "Architectural Styles and the Design of Network-based Software Architectures"
]

---
class: center, middle

# Regardless of Style, Understand your Tools

???
- Make it easy for yourself to learn
- Don't fight with your tools while learning
- Read man Pages
- Learn your shell
- Bootcamps and Ruby

--
a.k.a `man $tool` and `--help` all the things!

--

 http://overthewire.org/wargames/

---
class: center, middle, inverse
# Deliberate Practice

---

# Vulnhub.com

--

- Use the Walkthroughs
- Resist the feeling that it's 'cheating'

--

# Find Ongoing CTFs

--

- HackTheBox.eu
- CTF Archives

--

# Social Learning

--

* Live Events
* Communities
  - Meetup.com
  - NetSecFocus Mattermost - chat.netsecfocus.com

???
- Start with walkthroughs as intruction manuals
- After 2-4, try alone
- Creep scroll just enough to get unstuck

---
class: center, middle, inverse
# Learning Doesn't Stop With the Flag
---

.left-column[
# Keep it Going!

]
.right-column[
## How many ways can you explain it?
]
--
.right-column[
- Write it up!
]

--
.right-column[
## How many ways can you solve it?
]

--
.right-column[
- Are there other vectors?
- What about a different exploit?
]

--
.right-column[
## How would you solve this without tool X?
]

--
.right-column[
* Limiting your tools forces you to reconceptualize your approach
]

--
.right-column[
## How would I automate this?
]

--
.right-column[
* Think Deterministically
]

???
This one is my favorite. It's essentially a different version of 'How do you explain it?'

By automating the solution, you're forced to think about the problem in a deterministic way.

You encounter edge cases that could introduce more learning opportuinities along the way.

EX: Draw an Owl vs. Tell me what an Owl is

---
class: center, middle, inverse
# Show me!
  https://hackthebox.eu/invite

---
class: center, middle, inverse
# Dogfood
  https://hackthebox.eu/invite

---
class: middle
# Explain it

.paragraph[
>After inspecting the network traffic, some obfuscated code was found.
The code brought our attention to a function in the global scope, `makeInviteCode()`
This function POSTs to endpoint `/how/to/generate/invite` which returns some encoded JSON.
Upon decoding, we're instructed to POST to another endpoint. The response data is the encoded
invite code.
]

---
# How Else Can We Solve it?

--

#### -- Manually inspect all non-standard globally defined functions
#### -- Use Burp Suite to see calls that are made
#### -- Bruteforce the API endpoints

--

# What If We Can't Use Postman?

--

#### -- jQuery from the DevTools Console
#### -- curl
#### -- Python Requests
#### -- Ruby Net::HTTP

---
class: middle

# AUTOMATE IT!!

```bash
# API Endpoint Information Disclosure
1  curl -sL -X POST \
2    'https://www.hackthebox.eu/api/invite/how/to/generate' \
3    | jq '.data.data' \ # pull data.data property from resulting json
4    | tr -d '"' \       # delete all instances of the "
5    | base64 -d         # decode base64


#> In order to generate the invite code,
#> make a POST request to /api/invite/generate%


# Call 'hidden' endpoint
6  curl -sL -X POST \
7    'https://www.hackthebox.eu/api/invite/generate' \
8    | jq -r '.data.code' \ # I learned about -r making this slide!
9    | base64 -d

```

---

class: center, inverse, middle
# Resources
???
So many resources, but I'm only going to list a minimun so as to not overwhelm
---
class: middle
# CTF Events and Exercises

### NYU CTF Competitions - https://csaw.engineering.nyu.edu/

### CMU PPP-written challenges - https://picoctf.com/

### Embedded Security CTF - https://microcorruption.com/login

### Global CTF Leaderboards - https://ctftime.org

---
class: right middle
# Online Resources

### Vulnerable machines and walkthroughs

https://vulnhub.com

### Retired HackTheBox machines

https://youtube.com/ippsec

---
class: middle
.left-column[
# Topics
]
.right-column[
##**Reverse Engineering** - _Practical Reverse Engineering_
]
.right-column[
##**Scripting** - _Violent Python_
]

.right-column[
##**Web** - _Web Application Hackers Handbook_
]

.right-column[
##**Crypto** - _Applied Cryptography_
]

.right-column[
##**Binary Exploitation** - _Hacking: The Art of Exploitation_
]


.right-column[
##**All-In-One** - https://trailofbits.github.io/ctf/
]
---
class: center, inverse, middle
# Good Luck and Have Fun!
## * https://alexflor.es/ctf-talk
## * twitter/4lex

