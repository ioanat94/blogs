---
title: "Scout-A-Route Devlog #1 - Idea, Stack & Research"
datePublished: Sun Apr 14 2024 10:42:32 GMT+0000 (Coordinated Universal Time)
cuid: cluzeczhf000107jn4zmm6ck3
slug: scout-a-route-devlog-1-idea-stack-research
tags: programming-blogs, programming, devlog

---

I'm happy to share that I will be starting to work on a new side project, called Scout-A-Route! I've been feeling like working on a side project for some time now, but I didn't really have a good idea for anything (while there's nothing wrong with to-do apps and blog websites, those kinds of things don't really inspire or motivate me very much). In this first devlog I'll describe my idea and the current state of things.

---

## **Idea**

I go for a walk pretty much every day during the non-icy season, but I only really have a few routes that I keep repeating over and over. As you can imagine, it can get pretty boring and I sometimes feel the need for a change of scenery, but I don't really want to sit and plan a different route for myself every day either. So, I thought an app that randomly generates a route for me based on certain parameters would be helpful, as it keeps things fresh without me having to put much effort into coming up with routes every day.

### **MVP**

The application will display a map on one side and a sidebar on the other side. In the sidebar you can set up the parameters based on which the route will be generated, namely:

* starting point
    
* how much you want to walk, either in distance, time or steps
    

The app will generate a random loop route (meaning the end point will be the same as the starting point) based on the preferences provided. It will then display a "Open in Google Maps" option if you want to, for example, live track your position while walking and whatnot.

### **Future plans**

Some future plans I'm thinking about at the moment are:

* light/dark theme
    
* add biking alongside walking
    
* ability to sign up (probably via Google)
    
* save routes, waypoints and/or settings as favorites
    
* ability to set waypoints when setting up route preferences (use case example: I want to go on a 10.000 step walk but I want to stop by the grocery store somewhere along the way)
    
* possibly integrate with other apps (i.e. Strava, Komoot, and so on)
    

I'll probably come up with more along the way, and I'm also open to suggestions!

---

## **Stack**

Most of my experience so far is with React, Next.js and a bit of Astro and HTMX. I wanted to do something different for this project, and I've decided to give Svelte and SvelteKit a try. I have never used them but I always hear great things about them, so I thought it would be a good idea to use them for my project. I'll be using Tailwind and DaisyUI for styling, even though I am already quite familiar with these, because I love Tailwind too much and DaisyUI is a great component library for Tailwind. I'll also be using Vitest for unit testing and Playwright for end-to-end testing, because they come nicely packaged with the create-svelte CLI tool. The MVP will not require a database, but if I end up implementing sign up and the ability to favorite things, a document-based database like MongoDB will most likely suffice.

---

## **Research**

There are some technologies in this project that are new to me, so of course I had to do a little bit of research/learning before I got started.

### **Svelte/SvelteKit**

Svelte has a really nice tutorial on their website, for both Svelte and SvelteKit. It shows you basic and advanced things you can do with the framework, and it has a code editor built in so you can try things for yourself as you go. This has been a great resource and I love to see developers dedicated to teaching others how to use their tools. You can check it out here: [Svelte Tutorial](https://learn.svelte.dev/tutorial/welcome-to-svelte).

### **GitHub Projects**

I want some way to keep track of my project and the ideas and tasks that are a part of it. Since I'll be working on this alone, I don't really need anything fancy (to be honest, even a basic text file would have probably sufficed). But I've been meaning to check out GitHub Projects for a while and this seemed like a good opportunity for that. My conclusion after playing around with it for a bit is that it has many of the features that you would expect from a project management tool, but also many features are missing compared to other tools like Trello, Notion or Jira. But for the scope of my project it's more than enough, and I like the idea of keeping everything in one place, so I'll be using it for this project.

### **Google Maps API**

The Google Maps API is a huge service that allows you to use most of the Google Maps features within your own app. I've been reading mostly about the [Routes API](https://developers.google.com/maps/documentation/routes) and the [Directions API](https://developers.google.com/maps/documentation/javascript/directions), but I'm sure that actually using it in my project will be far more enlightening than simply reading the documentation. In other words, I'll be going with the flow with this one. :)

---

That's about it for this first devlog. It ended up being quite long but I expect future posts to be shorter, as I will probably work on this at a pretty slow pace (I already code every day for my job and I want to avoid getting burnt out). Thanks for reading and see you next time!

P.S.: The GitHub [repository](https://github.com/ioanat94/scout-a-route) and [project board](https://github.com/users/ioanat94/projects/4) are now public!