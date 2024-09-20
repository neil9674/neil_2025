---
layout: post
title: Student Home 
comments: true
---

## **About Me** 

> This is Neil's github page (neil_2025). I am a high school student at Del Norte High School, and I am currently in 10th grade.

<div>
</div>

<style>
    /* Style looks pretty compact, trace grid-container and grid-item in the code */
    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); /* Dynamic columns */
        gap: 10px;
    }
    .grid-item {
        text-align: center;
    }
    .grid-item img {
        width: 100%;
        height: 100px; /* Fixed height for uniformity */
        object-fit: contain; /* Ensure the image fits within the fixed height */
    }
    .grid-item p {
        margin: 5px 0; /* Add some margin for spacing */
    }
</style>

<!-- This grid_container class is for the CSS styling, the id is for JavaScript connection -->
<div class="grid-container" id="grid_container">
    <!-- content will be added here by JavaScript -->
</div>

<script>
    // 1. Make a connection to the HTML container defined in the HTML div
    var container = document.getElementById("grid_container"); // This container connects to the HTML div

    // 2. Define a JavaScript object for our http source and our data rows for the Living in the World grid
    var http_source = "https://upload.wikimedia.org/wikipedia/commons/";
    var living_in_the_world = [
        {"flag": "a/a4/Flag_of_the_United_States.svg", "greeting": "Hello", "description": "United States of America"},
        {"flag": "0/01/Flag_of_California.svg", "greeting": "Hey", "description": "California"},
        {"flag": "b/bb/Flag_of_North_Carolina.svg", "greeting": "How're you doing?", "description": "North Carolina"},
    ]; 
    
    // 3a. Consider how to update style count for size of container
    // The grid-template-columns has been defined as dynamic with auto-fill and minmax

    // 3b. Build grid items inside of our container for each row of data
    for (const location of living_in_the_world) {
        // Create a "div" with "class grid-item" for each row
        var gridItem = document.createElement("div");
        gridItem.className = "grid-item";  // This class name connects the gridItem to the CSS style elements
        // Add "img" HTML tag for the flag
        var img = document.createElement("img");
        img.src = http_source + location.flag; // concatenate the source and flag
        img.alt = location.flag + " Flag"; // add alt text for accessibility

        // Add "p" HTML tag for the description
        var description = document.createElement("p");
        description.textContent = location.description; // extract the description

        // Add "p" HTML tag for the greeting
        var greeting = document.createElement("p");
        greeting.textContent = location.greeting;  // extract the greeting

        // Append img and p HTML tags to the grid item DIV
        gridItem.appendChild(img);
        gridItem.appendChild(description);
        gridItem.appendChild(greeting);

        // Append the grid item DIV to the container DIV
        container.appendChild(gridItem);
    }
</script>

---

### Interests

> I like playing badminton and I am in the school Badminton team.
> I'm also a Life Scout in BSA, and I really enjoy camping and the outdoors.
> I also compete in Cyber Security competitions, and I am in the local Digital Security club.
> Lastly, I like following soccer.

<img src="pictureofeverything.png">

### Past

> I am a 2x National CyberPatriots winner, a cybersecurity competition.
> I am a life scout for BSA (almost Eagle Scout).
> Thats about it.

### Future

> I hope to get into the field of Cybersecurity, or another computer science field.
> Additionally, I really want to graduate high school.

### Fun
> I like playing video games, and listening to music.

<script src="https://utteranc.es/client.js"
        repo="neil9674/neil_2025"
        issue-term="title"
        label="blogpost-comment"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>