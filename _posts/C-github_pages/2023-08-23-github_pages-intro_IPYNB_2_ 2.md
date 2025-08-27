---
layout: post
title: Build a Themed Interactive Website
description: Learn how to create a themed mini-site using GitHub Pages, JavaScript, and Jupyter Notebooks.
categories: ['JavaScript']
permalink: /projects/interactive-site
type: ccc
courses: {'csse': {'week': 2}, 'csp': {'week': 2}, 'csa': {'week': 1}}
author: Your Name
menu: nav/interactive_site.html
---

# 🚀 Build a Themed Interactive Website Using GitHub Pages & JavaScript

Welcome to your Web Development mini-project! In this lesson, you'll learn how to build a fun and interactive site powered by **GitHub Pages**, **Jupyter Notebooks**, and **JavaScript**.

---

## 🎯 Learning Goals

By completing this project, you’ll be able to:

- Create and publish a multi-page website using GitHub Pages
- Design and build a **submenu navigation system**
- Embed **JavaScript interactivity** (random joke generator, quiz, etc.)
- Manage and share files through **Git & GitHub**
- Style your site using HTML & CSS

---

## 🧠 Project Theme: You Choose!

Pick a topic you enjoy or want to explore! Your site will be organized into sections based on your theme.

### 💡 Suggested Themes:

- 🎮 **Gaming Tips** – Mods, walkthroughs, Discords, etc.
- 🏋️ **Fitness Tracker** – Workouts, sleep/nutrition, progress charts
- 🐟 **Hobby Blog** – Raising pets, gardening, cooking, etc.
- 🤣 **Career Humor** – Explore jobs with a funny twist

---

## 🗂️ Project Structure

You’ll organize your project using a **submenu**, where each link leads to a themed subpage.

### 🧩 Required Features

| Feature | Description |
|--------|-------------|
| 🔗 Submenu | Custom navigation to link related topic pages |
| 📄 Custom Pages | Unique content under each submenu link |
| 📊 Interactivity | Use JavaScript to display dynamic content (e.g., random jokes) |
| 🎨 Styling | Add styles using CSS or GitHub themes |
| 🧪 Debugging | Use Developer Tools to inspect your code |

---

## ✍️ Brainstorm & Plan

Start by sketching out your idea.

### Example Theme: **Career Humor**

**Submenu Sections:**

1. Computer Science
2. Accounting
3. Journalism
4. Engineering
5. Astronomy
6. Film & Media

**Page Ideas:**
- Each page has themed jokes or fun facts
- Random joke generators powered by JavaScript
- Use of emojis, difficulty ratings, or “Did you know?” trivia

---

## 💻 JavaScript Example: Random Joke Generator

Here’s an example of how to create a random joke generator using JavaScript.

```javascript
var cs_jokes = [
  {
    joke: "Why was the computer cold? It left its Windows open.",
    explanation: "This is a pun. 'Windows' is a computer operating system, but it also means the glass windows in your house!"
  },
  {
    joke: "Why don’t computers take their hats off? Because they have CAPS LOCK on.",
    explanation: "'Caps Lock' is a keyboard key that types in capital letters — also a pun on wearing a cap (hat)!"
  },
  {
    joke: "Why did the computer go to art school? It wanted to learn how to draw its graphics.",
    explanation: "Computers use something called 'graphics cards' to show images — this joke is a silly play on that."
  },
  {
    joke: "Why couldn't the computer play soccer? It kept kicking the mouse!",
    explanation: "A computer mouse helps you click — but 'kicking the mouse' sounds like a sports move!"
  }
]

var index = Math.floor(Math.random() * cs_jokes.length);
var selected = cs_jokes[index];

console.log("Joke: " + selected.joke + " | Difficulty: " + selected.level);
