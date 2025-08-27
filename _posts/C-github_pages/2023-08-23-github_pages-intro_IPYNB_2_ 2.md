---
layout: post
title: GitHub Pages
description: The Web Programming topics are focused on learning Frontend programming, GitHub Pages, and Jupyter Notebooks.
categories: ['JavaScript']
permalink: /github/pages/intro
type: ccc
courses: {'csse': {'week': 2}, 'csp': {'week': 2}, 'csa': {'week': 1}}
author: John Mortensen
menu: nav/github_pages.html
---

# Build Your Own Info Website with GitHub Pages

Welcome! In this mini project, you and your programming partner will create an interactive information website using GitHub Pages. This is a great way to practice web programming skills while building something fun and useful.

---

## What You’ll Learn and Do

By the end of this project, you will:

- Create a **submenu** for easy navigation
- Organize your website content using submenu headings
- Design custom pages for each submenu topic
- Generate and display data relevant to your topic
- Add interactivity to your pages using JavaScript
- Explore the structure of a GitHub Pages site
- Experiment with styles and start debugging your pages

---

## Choosing Your Topic

Your website can be about anything you like! Here are some ideas to get you started:

- **Gaming Hub:** Showcase your favorite games, share tips, link to Discord groups, discuss mods, and more.
- **Fitness Tracker:** Outline your workout routines, track progress, and include tips about nutrition and sleep.
- **Pet Care:** Share information about raising pets or fish, record observations, and suggest helpful resources.
- **Career Humor:** Make a lighthearted site with jokes and fun facts about different careers.

---

## Brainstorming Together

Start by brainstorming ideas with your partner. Discuss what interests you and decide what your website will focus on.

Examples of brainstormed ideas:

- A blog about gaming strategies
- A fitness challenge tracker
- A guide to fish care
- A collection of career-related jokes

---

## Brainwriting: Career Humor Example

Let's say you pick **Career Humor** as your theme. Brainwriting means jotting down ideas quickly to organize them.

For Career Humor, you could create categories based on popular careers, such as:

1. Computer Science  
2. Accounting  
3. Journalism  
4. Film and Media  
5. Mechanical Engineering  
6. Biomedical Engineering  
7. Astronomy  

---

## Adding Fun Data: Jokes with JavaScript

You can add jokes or fun facts about each career category. Here’s an example of how JavaScript can randomly display a joke in the browser console:

```javascript
var csJokes = [
  { joke: "Why do computer scientists prefer the metric system? They are all pro-gram-ers!", difficulty: "Easy" },
  { joke: "Why do Java developers wear glasses? Because they can't C#.", difficulty: "Medium" },
  { joke: "Why do programmers prefer dark mode? Because light attracts bugs.", difficulty: "Easy" },
  { joke: "Why was the developer's code so clean? Because he used a broom() function.", difficulty: "Hard" },
  { joke: "Why did the programmer quit his job? Because he didn't get arrays.", difficulty: "Medium" }
];
var randomIndex = Math.floor(Math.random() * csJokes.length);
console.log("Here's a joke: " + csJokes[randomIndex]);
