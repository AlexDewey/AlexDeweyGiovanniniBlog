---
title: "Thrown into the Deepend: A Guide to Microprocessors with Internet Connectivity"
date: 2026-05-25
---

"I'm smart so I can figure it out" is a very good way to live your life. Too many engineers don't want to delve into unfamiliar topics, however I really enjoy expanding my wheelhouse and challenging myself where possible.

My first job outside of college was something completely different from the python ML/DS code I was used to. This is expected to a degree, as college more importantly focuses on teaching you how to think, and graduate school for me taught me how to research. So when this job involved using c++, microprocessors, networking, and scalable, low maintenance infrastructure, it pushed all the skills college had indirectly taught me.

My employer essentially just asked if I could make a product for him. With little to no idea of how to bring it to life, I said yes and started reading through articles, textbooks, anything I could get my hands on to make it a reality.

Not only was this a technical challenge, but I got to flex my social skills in how I liked to portray myself; someone who always said yes, delivered on impossible tasks, and did so maturely with a good attitude and clear communication.

![Alt text](https://raw.githubusercontent.com/AlexDewey/AlexDeweyBlog/main/_posts/images/Microprocessor/bestdiagram.png)

The biggest stressor by far was "I don't know what I don't know". In the past, and even now oftentimes the best way to learn is to make the mistake we wish to avoid. However with this project mistakes were costly. Time and money were issues, so if I ordered an incorrect part, was developing code for a microprocessor that wouldn't suffice due to a plethora of concerns ranging from energy, sim card/network compatibility, or a war with Iran that drastically delayed certain parts from shipping we'd be screwed. Jeff Bezos argued that the higher up you go, the less decisions you have to make, but the consequences of those decisions were much greater, and I felt that.

So what were those hard decisions?

Device: We use the walter-esp32s3 for low power consumption, and bluetooth/lte-m connectivity.
Language: We use c++ for efficiency and low power consumption. We have github repos of some examples we can draw from and send our data using an MQTT protocol.
Antenna: We connect a u.fl connector head to an IP67 antenna with a bulkhead in the middle. This ensures our antenna will withstand the elements effectively. We also have to take into consideration the band range that communicates with the towers effectively.
Sim Card: We utilize soracom.io sim cards due to their compatibility and partnership with the walter device alongside their extensive coverage in areas we sell to.
Cloud Infrastructure: We go with AWS systems due to their ability to encapsulate a large, sustainable ecosystem that interconnects with one another seamlessly, scales easily, and is reliable and user-friendly enough for non-technical people to operate.

Do I have regrets? Some. A lot of those decisions came down to a balancing act of time, money, and technical expertise. Because I was new to everything, needed to deliver quickly and on a tight budget, my decisions had to reflect these realities, as any misstep could spell catastrophe.

The device had to have bluetooth connectivity not for practical reasons, but for advertising reasons (better business value). This drove up the cost and power cost. There was a large ecosystem and support for the device, but if I were more capable individually with networking, a simpler device may have been better, at the cost of time.
The antenna had to be IP67, and while it serves very well and is relatively inexpensive, I'm not an electrical engineer and there could've been easily a better deal I wasn't aware of that did more. As of right now, the antenna is larger than what was desired.
The sim card service I chose was only chosen given the partnership mentioned before. There could've easily been a better, cheaper alternative with better coverage.
The cloud infrastructure being AWS was a balancing act of cost and convenience and time, as was most things. To move faster and be safer, we may sacrifice some cost savings.


The device itself mostly exists in sleep mode, only turning on to record signals and send and receive reports. Because I was incorporating TLS certificates, and there not being any examples of exactly what I wanted to do, I spent a lot of my time reading modem code, deciphering what code did what. "Was this value returning true because the function succeeded, or just because it didn't fail?" "What do each of these enum definitions relate to?" "How do I understand this at sign modem code to work?" "How do I effectively test for this part of the connection to be working correctly if no function explicitly allows for me to check?" Even small issues that would destroy the entire project, like a missing newline ascii character at the end of a TLS certificate would destroy the entire project. Luckily Claude was actually useful in diagnosing niche issues I hadn't a clue about like this, or suggestions like delaying certain code to allow for connections to occur.

On that subject, AI is great for exactly the opposite reason people want to use it for; disagreeing. An AI giving a solution is catastrophic because if wrong, will derail everything. An AI instead giving criticism means that it's okay if the criticism is incorrect, because even then it still fleshes out my understanding. In that way of utilizing AI, we avoid "comprehension debt", in that we don't know how the code works and we reap all the benefits and speed that AI gives us. I utilize AI in always combative instances, so that neither my code, nor my brain atrophies. Every decision I made I wanted the AI to say what could go wrong, or why my decision could fail; I was patching holes and reinforcing parts that could fail to reduce uncertainty.

Also I wanted to thank the walter team. Without their stellar documentation this project would've taken twice as long.
