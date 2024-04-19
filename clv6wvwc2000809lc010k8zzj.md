---
title: "Scout-A-Route Devlog #3 - Figma & Starting to Code"
datePublished: Fri Apr 19 2024 16:55:31 GMT+0000 (Coordinated Universal Time)
cuid: clv6wvwc2000809lc010k8zzj
slug: scout-a-route-devlog-3-figma-starting-to-code
tags: programming-blogs, programming, devlog

---

### **Planning**

As I mentioned in the previous devlog, the next thing I had to do was some planning, so I brainstormed a list of tasks and grouped them into a few categories. You can see the result below. Once I actually started coding I ended up with a few more tasks in addition to these.

![backlog](https://i.imgur.com/eCNOrQY.png align="left")

### **Figma**

Once I tried to actually start writing some code and making some components, I realized I'm not quite sure what I'm doing in terms of design. That's why I thought I should first make a very rough Figma design, not as a strict guideline for how the app should look, but rather to get an idea of what should go where, what size does everything need to be, what kind of inputs, buttons and colors I need, and so on. Below is a screenshot of what I ended up with, as you can see there's a few placeholder elements like the logo and the theme toggle. But like I said, this is just meant to be a rough guideline so that I have an easier time starting out.

![figma](https://i.imgur.com/cAoGwdR.png align="left")

### **Starting to Code - Route Form**

It's finally time to write some code! I started with the route form: the markup, styling, testing plus a basic API endpoint that currently just returns a string (this will later become the endpoint that will generate the actual route). Even though this was all quite basic, it was still a bit trickier than usual because I'm using Svelte and SvelteKit for this project, neither of which I have any previous experience with. Nevertheless, I got it working and it's been fun learning new approaches!

![route-form](https://i.imgur.com/6EHT44K.png align="center")

![playwright](https://i.imgur.com/LDbhKH2.png align="center")

### **Next steps**

Next I'll be adding my header and footer, both of which should be pretty straightforward, plus some more tests. After that I'll have to implement the "Click on the map to choose" part of my route form, which will enable users to choose their starting location. Thanks for reading and see you next time!