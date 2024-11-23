
Hey there! You probably noticed this is not a very active place, I still post repositories and snippets from time to time. In another time I used to contribute to projects using the monchitos82 account. 

## About me (02/24)

I have been a computer systems engineer for the past two decades. I have some knowledge in things like Operating Systems Administration, Software Development, Infrastructure Engineering and Site Reliability. All those catchy terms just mean I can deal with computers at a large number (I can also play with raspberries), write code to run them and understand what it takes to keep them running for more than a day.
I have worked in the financial world, consulting, gaming and recently in the internet industry. I like to meet people although I am not the most extrovert and I like to spend time learning about things related to technology and the industries I work with. I enjoy mentoring, but I am more of a jack of all trades so I end up learning more from others.

I have been lucky enough to have an education at many levels in many countries and continued that streak with my professional life.

I may come back here from time to time and speak of things I have in my mind. I don't contribute to any other social media platforms, I like to be the only loon in my feed, so yeah that's it.

## Simplicity is king in my world (02/24)

In the gist of many things going on lately around my own life I come close in contact with a lot of complaints about how things keep degrading in quality and surging in price and I keep reaching over and over again to the same conclusion: simple was, is and will always be better. Focusing on shells full of gimmicks tends to always give us the same outcome yet we often just don't get it. I usually am triggered by buzzwords like _slice and dice_ or _democratize_ but I come to really sympathize with this one: _enshitification_.

I like my code with zero boilerplate, my internet with zero limits, my services with zero subscriptions and the list goes on. I am not against progress, progress is good, that's why cars are safer and phones are faster, yet this decade all we get are flashy pinatas solving no problem, but the problem created to keep the greedy appeased. I never realized how much I miss what is simple and reliable. Screw those flashy trims and non-sense all glued together gadgets, let's go back to simple, there's where beauty of crafting lies, that's where we have control.

## Is my connection the issue? (07/24)

Recently I got this as feedback from an interview: _"Your internet connection seems poor"_. I was concerned about it since I want to work remotely when the chance is there without driving my family crazy by hogging the network. I knew I had 150 symmetric Mbps, so what's wrong then? Well, I had no clue, but I could start by monitoring and a quick search got me this neat python library: [speedtest-cli](https://github.com/sivel/speedtest-cli/wiki), so the nerd in me took the chance to write a prometheus sensor and poll the metric constantly. I wrote a non-prod-ready **[gist](https://gist.githubusercontent.com/mon-gmx/8b70cc44a4bf37c0015db1000fb83abc/raw/24ab84640b7c25dc11d002b9940f59f6a8ce7dae/speed_test_sensors.py)** for that matter that paired to a systemd service:

```
  [Unit]
  Description=speedtest

  [Service]
  Type=simple
  User=speedtest
  WorkingDirectory=/var/lib/speedtest
  ExecStart=/var/lib/speedtest/venv/bin/python /var/lib/speedtest/speed_test_sensors.py
  Restart=on-abort

  [Install]
  WantedBy=multi-user.target
```

got me monitoring my speed in no time. Now to what matters: it is not my connection the one that sucks, yes, it is slow by today's standards, but never degraded below the 90Mbps in any direction, and that's why data trumps everything and why observability is a must whenever dealing with problems where the root cause is not so evident. Will I dig further here? Hell yes, I have `iperf` measuring different latencies between different antennas (my network is simple: `modem -> router -> repeaters (mesh) -> computers`).

![image](https://github.com/user-attachments/assets/cf43a151-92e6-4a1b-9288-5a0eeb6b94d1)

### What I miss from our life in America (07/24)

America is a difficult place. It is a country that is built to test you, the place where you can be the best version of yourself and the place where you can meet your worst fate. Yet I think America is unique and I miss a lot from it. I don't miss its savage health system or its weirdness regarding races and mindsets. I miss what freedom means there, I miss its people and I miss what its people made of it. I don't feel sorry or regret about leaving America, after all, it never felt like home to me. I think America is a great example of what a country can be, except it is hard to understand it unless you've been there for longer than a vacation. The love of the land, the make it work no matter what, the do it right and do it best mindsets are what I miss the hardest. I wish my country had some vague resemblance to those ideas.

### My two cents on "coding" interviews (07/24)

Yes I am one more of those guys. I see no benefit to them other than stress the shit out of a person to no good end. I would say I am the same as happy doing these interviews as I am creating 1 machine cluster using kubernetes. Two of the most enjoyable interview processes I had (and memorable since they really demanded more skills than memorizing algorithms or snooping over the answers tab) were with Klarna and Wizeline; Klarna asked me not only to provide complex functions but to actually write a service to query those functions and emit metrics for them (2 days given for the task) and Wizeline asked me to write a function in a language they invented so they could evaluate my ability to learn and work with what I learned (no guy on the other side of the terminal). I wish I could mention Apple, Amazon, Google, Microsoft of Meta here, but nope, they all do the same silly dance, so I dare to say that I don't see this inventive anywhere in big tech, I know, the process was created to pick the brightest but just as with immigration, it is gamed and not fun at all. So I am done with this nonsense, even if I had to give up my career, I will always push back on it. Not saying puzzles are crap, they are not, but using them as the first step to filter out the competence of a candidate based on algorithms and problems that they may not need it's more of a bluff than a real need.

### A small parenthesis on cpacity (09/24)

I will start this one by posting a term I forgot to mention in a recent conversation: **load testing**

Capacity planning is a very interesting discussion; it requires knowing where you're standing and where you're going. I just had a conversation where we discussed vertical vs. horizontal escalation. But the conversation can only start when you know where you are standing and for that understanding to happen, you need to know what are your current limits, that's where load testing comes into play. Yes, you will add buffering in different layers to disperse the load and you will break the problem you try to solve to improve your ability to scale, but that is step number two.

### Why ChatGPT is (for now) my best pair programming amigo (11/24)
Using ChatGPT to code is like shooting at your own feet, except that IMO, it has been the best companion ever. I would guess co-pilot would be fairly efficient, but I am budget restricted to try it. Anyway, I find the capacity of bouncing ideas with the GAI a big up that if handled with care can boost productivity.
Unlike using stackoverflow, which I despise, ChatGPT will lay the mines right under your feet. They will blow before you ship, which is a good thing to find out. If you are careful enough with what you ask for, with reading what you got served and with being critical to the response, probably you can get better code. Not saying it is easy though, GPT is terribly bad at getting good and consistent unit tests, however it is brilliant at providing useful mocks so that's a big tradeoff.
So what am I suggesting here? Should you replace all your tools for using ChatGPT? Nah, but there are a few you for sure will want to get rid off: Google being the first one. If you can search through your prompt, the only other thing you need is access to github (GPT is not actual and deprecation and old code are no strange to it). So having the changelog, API descriptions and a peer that reviews your ideas is like a powerful trifecta, that in my case, has helped me ship at least 5 projects in less than a couple months. Am I grateful for it? You bet! Am I afraid it will replace me? Nah, it will get better when it can handle context and when that happens, I will be grateful for the transition :robot:💙
I mentioned before it is a good mentor, but what's remarkable of all of this, is that if you pay close attention, you are setting the pace and you are reasoning with yourself, it is like looking into a warped mirror to get a fresh perspective of what you can actually do with a little better education.
