---
layout: base
title: Student Home 
description: Home Page
author: Neil Chandra
image: /images/mario_animation.png
hide: true
---

{% include nav/home.html %}

<!-- Liquid:  statements -->

<!-- Include submenu from _includes to top of pages -->
<!--- Concatenation of site URL to frontmatter image  --->
{% assign sprite_file = site.baseurl | append: page.image %}
<!--- Has is a list variable containing mario metadata for sprite --->
{% assign hash = site.data.mario_metadata %}  
<!--- Size width/height of Sprit images --->
{% assign pixels = 256 %}

<!--- HTML for page contains <p> tag named "Mario" and class properties for a "sprite"  -->

<p id="mario" class="sprite"></p>
  
<!--- Embedded Cascading Style Sheet (CSS) rules, 
        define how HTML elements look 
--->
<style>

  /*CSS style rules for the id and class of the sprite...
  */
  .sprite {
    height: {{pixels}}px;
    width: {{pixels}}px;
    background-image: url('{{sprite_file}}');
    background-repeat: no-repeat;
  }

  /*background position of sprite element
  */
  #mario {
    background-position: calc({{animations[0].col}} * {{pixels}} * -1px) calc({{animations[0].row}} * {{pixels}}* -1px);
  }
</style>

<!--- Embedded executable code--->
<script>
  ////////// convert YML hash to javascript key:value objects /////////

  var mario_metadata = {}; //key, value object
  {% for key in hash %}  
  
  var key = "{{key | first}}"  //key
  var values = {} //values object
  values["row"] = {{key.row}}
  values["col"] = {{key.col}}
  values["frames"] = {{key.frames}}
  mario_metadata[key] = values; //key with values added

  {% endfor %}

  ////////// game object for player /////////

  class Mario {
    constructor(meta_data) {
      this.tID = null;  //capture setInterval() task ID
      this.positionX = 0;  // current position of sprite in X direction
      this.currentSpeed = 0;
      this.marioElement = document.getElementById("mario"); //HTML element of sprite
      this.pixels = {{pixels}}; //pixel offset of images in the sprite, set by liquid constant
      this.interval = 100; //animation time interval
      this.obj = meta_data;
      this.marioElement.style.position = "absolute";
    }

    animate(obj, speed) {
      let frame = 0;
      const row = obj.row * this.pixels;
      this.currentSpeed = speed;

      this.tID = setInterval(() => {
        const col = (frame + obj.col) * this.pixels;
        this.marioElement.style.backgroundPosition = `-${col}px -${row}px`;
        this.marioElement.style.left = `${this.positionX}px`;

        this.positionX += speed;
        frame = (frame + 1) % obj.frames;

        const viewportWidth = window.innerWidth;
        if (this.positionX > viewportWidth - this.pixels) {
          document.documentElement.scrollLeft = this.positionX - viewportWidth + this.pixels;
        }
      }, this.interval);
    }

    startWalking() {
      this.stopAnimate();
      this.animate(this.obj["Walk"], 3);
    }

    startRunning() {
      this.stopAnimate();
      this.animate(this.obj["Run1"], 6);
    }

    startPuffing() {
      this.stopAnimate();
      this.animate(this.obj["Puff"], 0);
    }

    startCheering() {
      this.stopAnimate();
      this.animate(this.obj["Cheer"], 0);
    }

    startFlipping() {
      this.stopAnimate();
      this.animate(this.obj["Flip"], 0);
    }

    startResting() {
      this.stopAnimate();
      this.animate(this.obj["Rest"], 0);
    }

    stopAnimate() {
      clearInterval(this.tID);
    }
  }

  const mario = new Mario(mario_metadata);

  ////////// event control /////////

  window.addEventListener("keydown", (event) => {
    if (event.key === "ArrowRight") {
      event.preventDefault();
      if (event.repeat) {
        mario.startCheering();
      } else {
        if (mario.currentSpeed === 0) {
          mario.startWalking();
        } else if (mario.currentSpeed === 3) {
          mario.startRunning();
        }
      }
    } else if (event.key === "ArrowLeft") {
      event.preventDefault();
      if (event.repeat) {
        mario.stopAnimate();
      } else {
        mario.startPuffing();
      }
    }
  });

  //touch events that enable animations
  window.addEventListener("touchstart", (event) => {
    event.preventDefault(); // prevent default browser action
    if (event.touches[0].clientX > window.innerWidth / 2) {
      // move right
      if (currentSpeed === 0) { // if at rest, go to walking
        mario.startWalking();
      } else if (currentSpeed === 3) { // if walking, go to running
        mario.startRunning();
      }
    } else {
      // move left
      mario.startPuffing();
    }
  });

  //stop animation on window blur
  window.addEventListener("blur", () => {
    mario.stopAnimate();
  });

  //start animation on window focus
  window.addEventListener("focus", () => {
     mario.startFlipping();
  });

  //start animation on page load or page refresh
  document.addEventListener("DOMContentLoaded", () => {
    // adjust sprite size for high pixel density devices
    const scale = window.devicePixelRatio;
    const sprite = document.querySelector(".sprite");
    sprite.style.transform = `scale(${0.2 * scale})`;
    mario.startResting();
  });

</script>

## **Home** 🏠

### Nighthawk CSP Link for Help 💻
<a href="https://nighthawkcoders.github.io/portfolio_2025/navigation/section/csp">Visit the Nighthawk CSP Page</a>

### [Sprint 2 Final Project](https://neil9674.github.io/neil_2025/2024/10/16/Connect4_Game_IPYNB_2_.html)

<style>
    #summaryTable {
        border-collapse: collapse;
        width: 60%;
        border: 2px solid cyan;
        display: inline-block;
    }
    #summaryTable th, #summaryTable td {
        border: 1px solid cyan;
        text-align: center;
        padding: 0;
        height: 100px;
        width: 200px;
        background-color: #222;
        color: #00f;
    }
    #summaryTable a {
        color: #00f;
        text-decoration: none;
    }
    .summary {
        display: none;
        position: absolute;
        background-color: #444;
        color: white;
        padding: 10px;
        border: 1px solid cyan;
        width: 200px;
        z-index: 10;
        font-size: 18px;
        left: 70%;
        top: 10%;
    }
</style>
<table id="summaryTable">
    <tr>
        <td><a href="https://neil9674.github.io/neil_2025/2024/10/08/BigIdea3-Section1_IPYNB_2_.html" onmouseover="showSummary('Variables are used to store data values. They can be changed during program execution.')" onmouseout="hideSummary()">Variables</a></td>
        <td><a href="https://nighthawkcoders.github.io/portfolio_2025/csp/big-idea/p2/3-2/" onmouseover="showSummary('Data abstraction is a concept that hides complex realities while exposing only the necessary parts. It simplifies programming by reducing complexity.')" onmouseout="hideSummary()">Data Abstraction (Lesson Taught)</a></td>
        <td><a href="https://neil9674.github.io/neil_2025/2024/10/09/BigIdea3-Section3_IPYNB_2_.html" onmouseover="showSummary('Mathematical expressions are combinations of numbers, variables, and operators. They are used to perform calculations and operations.')" onmouseout="hideSummary()">Mathematical Expressions</a></td>
    </tr>
    <tr>
        <td><a href="https://neil9674.github.io/neil_2025/2024/10/08/BigIdea3-Section4_IPYNB_2_.html" onmouseover="showSummary('Strings are sequences of characters used to represent text.')" onmouseout="hideSummary()">Strings</a></td>
        <td><a href="https://neil9674.github.io/neil_2025/2024/10/09/BigIdea3-Section5_IPYNB_2_.html" onmouseover="showSummary('Boolean expressions evaluate to true or false. They are fundamental in decision-making processes in programming.')" onmouseout="hideSummary()">Boolean Expressions</a></td>
        <td><a href="https://neil9674.github.io/neil_2025/2024/10/10/BigIdea3-Section7_IPYNB_2_.html" onmouseover="showSummary('Conditionals are statements that execute different actions based on whether a specified condition is true or false. They are essential for controlling the flow of a program.')" onmouseout="hideSummary()">Conditionals</a></td>
    </tr>
    <tr>
        <td><a href="https://neil9674.github.io/neil_2025/2024/10/10/BigIdea3-Section6_IPYNB_2_.html" onmouseover="showSummary('Nested conditionals are conditionals placed inside another conditional. They allow for more complex decision-making in programming.')" onmouseout="hideSummary()">Nested Conditionals</a></td>
        <td><a href="https://neil9674.github.io/neil_2025/2024/09/03/BigIdea3-Section8_IPYNB_2_.html" onmouseover="showSummary('Iteration refers to the process of repeating a set of instructions a specified number of times or until a certain condition is met. In this lesson, we used both while loops and for loops.')" onmouseout="hideSummary()">Iteration</a></td>
        <td><a href="https://neil9674.github.io/neil_2025/2024/09/03/BigIdea3-Section10_IPYNB_2_.html" onmouseover="showSummary('List operations involve manipulating data stored in lists. Common operations include adding, removing, and accessing elements in a list.')" onmouseout="hideSummary()">List Operations</a></td>
    </tr>
</table>

<div class="summary" id="summaryBox"></div>

<script>
    function showSummary(text) {
        const summaryBox = document.getElementById('summaryBox');
        summaryBox.innerHTML = text;
        summaryBox.style.display = 'block';
    }

    function hideSummary() {
        const summaryBox = document.getElementById('summaryBox');
        summaryBox.style.display = 'none';
    }

    const table = document.getElementById('summaryTable');
    const summaryBox = document.getElementById('summaryBox');
    const rect = table.getBoundingClientRect();
    summaryBox.style.left = (rect.right + 10) + 'px';
    summaryBox.style.top = rect.top + 'px';
</script>






### [Sprint 1](https://neil9674.github.io/neil_2025/2024/08/21/sprint1_plan_IPYNB_2_.html); Weeks 0 - 3
> Notebooks
> - [Jupyter Notebook Hacks](https://neil9674.github.io/neil_2025/2024/09/08/Jupyter-Notebook-Hack_IPYNB_2_.html)
> - [Pair Programming Project](https://neil9674.github.io/neil_2025/2024/09/08/Cookie_Clicker-(PairProject).html)
> - [Tools and Equipment Play Hacks](https://neil9674.github.io/neil_2025/2024/09/08/Tools_Equipment_Play-Hack_IPYNB_2_.html)
> - [Frontend Hacks](https://neil9674.github.io/neil_2025/2024/09/08/Frontend_Hacks.html)

> Projects
> - [Cookie Clicker](https://neil9674.github.io/neil_2025/2024/09/08/Cookie_Clicker-(PairProject).html)
> - [Tic Tac Toe](https://neil9674.github.io/neil_2025/2024/09/23/TicTacToe.html)
> - [Snake](https://neil9674.github.io/neil_2025/snake/)
> - [Rock, Paper, Scissors](https://neil9674.github.io/neil_2025/2024/09/19/github_pages_hacks_javascript_IPYNB_2_.html)