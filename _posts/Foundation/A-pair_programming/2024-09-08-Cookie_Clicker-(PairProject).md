---
layout: post
title: Pair Programming (Cookie Clicker) - Neil C
type: issues
toc: true
description: This is a Cookie Clicker that was made for the Pair Programming Project. I collaborated with my peer and asked them for feedback on this code.
---

<div>
    <h3> Cookie Clicker </h3>
    <p> Click the cookie as many times as possible, you can see your score on the left of the cookie. Have fun. </p>
</div>

<img alt="describe image" src="{{site.baseurl}}/workspaces/neil_2025/images/cookie.png" width="100" height="200">
<p>Image clicked <span id="clickCount">0</span> times.</p>

<script>
    let count = 0;
    const image = document.getElementById('clickableImage');
    const display = document.getElementById('clickCount');

    image.addEventListener('click', () => {
        count++;
        display.textContent = count;
    });
</script>

<div>
    <p></p>
</div>